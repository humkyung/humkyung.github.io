---
title: nginx proxy 설정
date: 2026-02-06
categories:
  - n8n
tags:
  - nginx
  - proxy
img_path: /assets/images/
---
현재 의뢰를 받아 Web 어플리케이션을 개발하고 있는데, 보안 상의 이유로 nginx를 통해서만 backend에 접속하도록 수정하였습니다. 이전에는 backend의 api 주소가 노출되었습니다.

---
### 🛠️ 시스템 구성

- **Backend:** Sprint Boot   
- **Frontend:** React
- **Database:** MS-Sql
 
---

Backend, Frontend 둘 다 같은 docker(Docker Desktop)에 올라와 있습니다. Backend, Frontend Docker를 생성할 때 동일한 네트워크에 묶어줘야 합니다. Dockerfile 상단에 추가합니다.
```bash
# 네트워크가 없으면 생성
if (!(docker network ls -q -f name=my-net)) {
    Write-Host "Creating network: my-net"
    docker network create my-net
}
```

```shell
docker network inspect my-net
```
Docker를 생성했다면 커맨드 창에서 위 명령어로 my-net에 대한 정보를 확인할 수 있습니다.

Backend, Frontend가 구성되었으면 nginx.conf에서 proxy 설정하여 /api/가 포함된 요청이 들어오면 Backend로 전달하여 처리하도록 합니다.
**proxy_pass** 설정할 때 앞서 생성한 Backend Docker 이름을 기입해야 합니다.
```shell
server {
	listen 80;
	server_name localhost;

	location / {
		root /usr/share/nginx/html;
		index index.html index.htm;
		# SPA(Single Page Application) 라우팅을 위해 필요
		try_files $uri $uri/ /index.html;
	}
  
	# Backend API 프록시 설정
    location /api/ {
		# Spring Boot 기본 포트가 8080이라고 가정합니다.
        proxy_pass http://BackendName:8080;

        # 헤더 전달 (IP 추적 등을 위해 필수)
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # 타임아웃 설정 (필요 시 늘리세요 - 엑셀 업로드 등)
        proxy_read_timeout 300s;
        proxy_connect_timeout 300s;
    }
}
```

마지막으로 .env.production 파일을 확인합니다.
이전에 입력된 Backend API 서버 주소를 삭제합니다.

```shell
# [수정 전] 백엔드로 직접 접속 (Nginx 우회, CORS 위험)
# NEXT_PUBLIC_API_SERVER=http://localhost:8090

# [수정 후] 빈 값으로 설정 (추천)
# 빈 값으로 두면 브라우저는 API 요청을 '/api/...' 상대 경로로 보냅니다.
# 즉, http://localhost:3000/api/... 로 요청이 가고, Nginx가 이를 잡아 백엔드로 넘깁니다.
NEXT_PUBLIC_API_SERVER=

# 만약 빈 값이 동작하지 않는 구조라면 아래처럼 Frontend 주소를 적으세요.
# NEXT_PUBLIC_API_SERVER=http://localhost:3000

# -----------------------------------------------------------

# [SSE 설정]
# SSE(알람)도 Nginx를 통하게 하려면 동일하게 설정합니다.
# 단, Nginx에서 SSE 헤더 설정이 필요할 수 있습니다. 
# 일단 API 서버 설정과 맞추는 것이 좋습니다.
NEXT_PUBLIC_SSE_SERVER=
```
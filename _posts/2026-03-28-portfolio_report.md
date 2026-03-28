---
layout: none
title: 2026년 3월 28일 포트폴리오 보고서
date: 2026-03-28
categories:
  - 금융
tags:
  - 포트폴리오
  - portfolio
img_path: /assets/images/
---
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>📊 AI 투자비서 — 포트폴리오 가치평가 리포트 2026.03.28</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
:root{--blue:#1a56db;--bl:#e8f0fe;--green:#0d9f6e;--gl:#d5f0e8;--red:#dc2626;--rl:#fee2e2;--amber:#b45309;--al:#fef3c7;--gray:#374151;--grl:#f9fafb;--brd:#e5e7eb;--tx:#111827;--tx2:#6b7280;--sh:0 1px 4px rgba(0,0,0,.1);--purple:#7c3aed;--pl:#f3e8ff}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,'Malgun Gothic',sans-serif;background:#f3f4f6;color:var(--tx);line-height:1.65}
.hdr{background:linear-gradient(135deg,#0f2550,#1a56db 60%,#1e429f);color:#fff;padding:36px 24px 28px;text-align:center}
.hdr .badge{display:inline-block;background:rgba(255,255,255,.18);border-radius:20px;padding:4px 14px;font-size:12px;margin-bottom:10px}
.hdr h1{font-size:26px;font-weight:800;margin-bottom:6px}
.hdr .sub{font-size:13px;opacity:.75}
.hdr .kpi{display:flex;justify-content:center;gap:28px;margin-top:20px;flex-wrap:wrap}
.hdr .kpi-item .v{font-size:21px;font-weight:700}
.hdr .kpi-item .l{font-size:11px;opacity:.65;margin-top:2px}
.wrap{max-width:960px;margin:0 auto;padding:20px 14px}
.card{background:#fff;border-radius:12px;padding:22px;margin-bottom:18px;box-shadow:var(--sh)}
.card-title{font-size:17px;font-weight:700;margin-bottom:14px;display:flex;align-items:center;gap:7px}
.pgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:9px;margin-bottom:14px}
.pitem{background:var(--grl);border:1px solid var(--brd);border-radius:8px;padding:10px 12px}
.pitem .pn{font-size:11px;color:var(--tx2);margin-bottom:2px}
.pitem .pv{font-size:15px;font-weight:700}
.pitem .ps{font-size:10px;color:var(--tx2)}
.pitem .pr{font-size:11px;font-weight:600}
.scard{border:1px solid var(--brd);border-radius:10px;margin-bottom:12px;overflow:hidden}
.shdr{display:flex;align-items:center;justify-content:space-between;padding:13px 16px;background:var(--grl);flex-wrap:wrap;gap:7px;cursor:pointer;user-select:none;transition:background .15s}
.shdr:hover{background:#ececec}
.sname{font-size:15px;font-weight:700}
.sticker{font-size:11px;color:var(--tx2);background:#fff;border:1px solid var(--brd);border-radius:5px;padding:2px 7px}
.smeta{display:flex;gap:10px;align-items:center;flex-wrap:wrap}
.sprice{font-weight:600;font-size:13px}
.sweight{font-size:11px;font-weight:700;background:var(--bl);color:var(--blue);padding:3px 9px;border-radius:10px}
.sbadge{font-size:12px;font-weight:700;padding:3px 10px;border-radius:16px}
.bg-high{background:var(--gl);color:var(--green)}
.bg-mid{background:var(--bl);color:var(--blue)}
.bg-low{background:var(--al);color:var(--amber)}
.bg-bad{background:var(--rl);color:var(--red)}
.sbody{padding:16px;display:none}
.sbody.open{display:block}
.tico{font-size:14px;transition:transform .2s}
.shdr.open .tico{transform:rotate(180deg)}
.stitle{font-size:12px;font-weight:700;color:var(--blue);margin:12px 0 7px;text-transform:uppercase;letter-spacing:.4px}
table{width:100%;border-collapse:collapse;font-size:12px;margin-bottom:10px}
th{background:var(--grl);padding:7px 9px;text-align:left;font-weight:600;border-bottom:1px solid var(--brd)}
td{padding:7px 9px;border-bottom:1px solid var(--brd)}
tr:last-child td{border-bottom:none}
.up{color:var(--green);font-weight:700}
.dn{color:var(--red);font-weight:700}
.ibox{padding:9px 13px;border-radius:6px;font-size:12px;margin-bottom:10px;border-left:3px solid}
.ibox.info{background:var(--bl);border-color:var(--blue)}
.ibox.warn{background:var(--al);border-color:var(--amber)}
.ibox.danger{background:var(--rl);border-color:var(--red)}
.ibox.ok{background:var(--gl);border-color:var(--green)}
.acard{border-radius:10px;padding:14px 16px;margin-bottom:11px}
.acard.sell{background:#fff5f5;border:1px solid #fecaca}
.acard.warn2{background:#fffbeb;border:1px solid #fde68a}
.acard.buy2{background:#f0fdf4;border:1px solid #bbf7d0}
.acard.hold{background:var(--bl);border:1px solid #bfdbfe}
.atitle{font-size:14px;font-weight:700;margin-bottom:5px}
.acard.sell .atitle{color:var(--red)}
.acard.warn2 .atitle{color:var(--amber)}
.acard.buy2 .atitle{color:var(--green)}
.acard.hold .atitle{color:var(--blue)}
.atag{display:inline-block;font-size:10px;font-weight:700;padding:2px 7px;border-radius:8px;margin-left:7px}
.acard.sell .atag{background:var(--red);color:#fff}
.acard.warn2 .atag{background:var(--amber);color:#fff}
.acard.buy2 .atag{background:var(--green);color:#fff}
.acard.hold .atag{background:var(--blue);color:#fff}
.acard ul{font-size:12px;color:var(--gray);padding-left:15px;margin-top:7px}
.acard li{margin-bottom:3px}
.sbar-wrap{display:flex;align-items:center;gap:9px;margin-bottom:8px;font-size:12px}
.sbar-lbl{min-width:110px;font-weight:500;text-align:right}
.sbar-track{flex:1;background:#e5e7eb;border-radius:4px;height:17px;overflow:hidden}
.sbar-fill{height:100%;border-radius:4px;display:flex;align-items:center;justify-content:flex-end;padding-right:5px;font-size:10px;font-weight:700;color:#fff}
.sbar-num{min-width:34px;font-weight:700}
.toc{display:grid;grid-template-columns:repeat(auto-fill,minmax(165px,1fr));gap:7px}
.toc-item{background:var(--grl);border:1px solid var(--brd);border-radius:8px;padding:9px 11px;cursor:pointer;font-size:12px;transition:background .15s}
.toc-item:hover{background:var(--bl)}
.toc-n{font-weight:700}
.toc-s{font-size:11px;color:var(--tx2)}
.ch-wrap{position:relative;width:100%;height:260px}
.news-wrap{background:#fff7ed;border:1px solid #fed7aa;border-radius:8px;padding:10px 14px;font-size:12px;margin-bottom:12px}
.news-wrap .nt{font-weight:700;color:#9a3412;margin-bottom:5px}
.ni{padding:5px 0;border-bottom:1px solid #fed7aa;color:var(--gray)}
.ni:last-child{border-bottom:none}
.ni b{color:var(--tx)}
.macro-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:10px;margin-bottom:14px}
.macro-item{background:var(--grl);border:1px solid var(--brd);border-radius:8px;padding:12px 14px}
.macro-item .mt{font-size:11px;color:var(--tx2);margin-bottom:4px;font-weight:600;text-transform:uppercase}
.macro-item .mv{font-size:16px;font-weight:700}
.macro-item .ms{font-size:11px;margin-top:3px}
.tag{display:inline-block;font-size:10px;padding:2px 7px;border-radius:8px;margin-right:3px}
.tag-b{background:var(--bl);color:var(--blue)}
.tag-g{background:var(--gl);color:var(--green)}
.tag-r{background:var(--rl);color:var(--red)}
.tag-a{background:var(--al);color:var(--amber)}
.tag-p{background:var(--pl);color:var(--purple)}
.alert-banner{background:linear-gradient(90deg,#7f1d1d,#991b1b);color:#fff;padding:10px 16px;border-radius:8px;font-size:13px;font-weight:700;margin-bottom:14px;display:flex;align-items:center;gap:8px}
.timeline{border-left:2px solid var(--brd);margin-left:8px;padding-left:16px}
.tl-item{position:relative;margin-bottom:14px}
.tl-item::before{content:'';position:absolute;left:-21px;top:5px;width:10px;height:10px;border-radius:50%;background:var(--blue);border:2px solid #fff}
.tl-item.red::before{background:var(--red)}
.tl-item.green::before{background:var(--green)}
.tl-item.amber::before{background:var(--amber)}
.tl-date{font-size:11px;color:var(--tx2);font-weight:600}
.tl-text{font-size:12px;color:var(--tx);margin-top:2px}
.ret-pos{color:var(--green);font-weight:700}
.ret-neg{color:var(--red);font-weight:700}
.ret-neu{color:var(--tx2);font-weight:600}
@media(max-width:600px){.hdr h1{font-size:20px}.hdr .kpi{gap:14px}.shdr{flex-direction:column;align-items:flex-start}}
.footer{text-align:center;padding:20px;color:var(--tx2);font-size:11px}
.radar-wrap{position:relative;width:100%;max-width:400px;height:380px;margin:0 auto}
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:16px}
@media(max-width:640px){.two-col{grid-template-columns:1fr}}
.section-divider{border:none;border-top:2px solid var(--brd);margin:20px 0}
</style>
</head>
<body>

<!-- ===== HEADER ===== -->
<div class="hdr">
  <div class="badge">🤖 AI 투자비서 자동 생성 리포트 v2.0</div>
  <h1>보유 종목 가치평가 &amp; 투자전략 리포트</h1>
  <div class="sub">기준일: 2026년 3월 28일 (토) | 데이터: Investing.com · Yahoo Finance · 증권사 컨센서스<br>USD/KRW ≈ 1,500 · WTI $93.66 · Fed 3.50~3.75% 동결 | ⚡ 미국-이란 전쟁 1개월 · 🔬 Google TurboQuant 쇼크</div>
  <div class="kpi">
    <div class="kpi-item"><div class="v">₩71,352,769</div><div class="l">총 포트폴리오 (예수금 포함)</div></div>
    <div class="kpi-item"><div class="v">17개</div><div class="l">보유 종목</div></div>
    <div class="kpi-item"><div class="v">₩858,503</div><div class="l">예수금 (1.2%)</div></div>
    <div class="kpi-item"><div class="v">AI·반도체·K-Pop</div><div class="l">핵심 포트폴리오 테마</div></div>
  </div>
</div>

<div class="wrap">

<!-- ===== 핵심 알림 ===== -->
<div class="card">
  <div class="card-title">🚨 이번 주 핵심 이슈 (2026.03.25~28)</div>
  <div class="alert-banner">⚡ ALERT: Google TurboQuant 발표 (3/25) → 삼성전자 -4.71% · SK하이닉스 -6.23% · Micron -3.4% 충격. 단기 과반응 판단, 장기 수요 훼손 제한적.</div>
  <div class="news-wrap">
    <div class="nt">📌 주요 이슈 (기준일: 2026.03.28)</div>
    <div class="ni">🔬 <b>Google TurboQuant (3/25 발표)</b>: AI 메모리 6배 압축, H100 8배 속도↑ 알고리즘. 반도체 주가 급락. 반론: "KV캐시 압축은 훈련 메모리가 아닌 추론 메모리만 → 장기 HBM 수요 훼손 제한. 저빈스의 역설(효율↑ → 사용량↑)."</div>
    <div class="ni">🎤 <b>BTS 광화문 컴백 공연 (3/21)</b>: 서울시 추산 4.8만명 집결 (예측 20~30만 대비 크게 미달). 하이브 주가 급락 ₩344,000→₩307,000. 단, 4/9 유료 스타디움 공연이 진짜 수요 시그널.</div>
    <div class="ni">🛢️ <b>미국-이란 전쟁 1개월 (3/28)</b>: WTI $93.66, 원달러 1,500~1,505원. 트럼프 10일 추가 공격 유예 발표. 한국 항공·화학 비상경영. 포트폴리오 내 USD 자산이 자연 헤지 역할.</div>
    <div class="ni">💰 <b>Fed 3월 FOMC 금리 동결</b>: 3.5~3.75% 유지. 2026년 연내 1회 인하 유지 전망. 6월 인하 확률 ~47%. 이란 전쟁 인플레 불확실성이 인하 지연 요인.</div>
    <div class="ni">🏥 <b>UnitedHealth(UNH) 급락 지속</b>: 평단 대비 -38.7% 손실. 미국 의료보험 규제 강화·손해율 급등이 원인. 포트폴리오 최대 손실 종목 중 하나.</div>
  </div>
</div>

<!-- ===== 거시경제 ===== -->
<div class="card">
  <div class="card-title">🌐 거시경제 환경 요약</div>
  <div class="macro-grid">
    <div class="macro-item">
      <div class="mt">🏦 미 연준 기준금리</div>
      <div class="mv">3.50~3.75%</div>
      <div class="ms" style="color:var(--amber)">3월 동결. 연내 1회 인하 전망. 6월 확률 47%.</div>
    </div>
    <div class="macro-item">
      <div class="mt">💵 USD/KRW 환율</div>
      <div class="mv" style="color:var(--red)">~1,500원</div>
      <div class="ms" style="color:var(--red)">2009년 이후 최약세. 중동 전쟁·에너지 비용 압박.</div>
    </div>
    <div class="macro-item">
      <div class="mt">🛢️ WTI 유가</div>
      <div class="mv" style="color:var(--red)">$93.66</div>
      <div class="ms" style="color:var(--amber)">미-이란 전쟁. 협상 진전 시 $80대 복귀 가능.</div>
    </div>
    <div class="macro-item">
      <div class="mt">📊 미국 PCE 물가(2월)</div>
      <div class="mv" style="color:var(--amber)">2.7% (YoY)</div>
      <div class="ms">3월 FOMC 상향. 인하 시기 지연 요인.</div>
    </div>
    <div class="macro-item">
      <div class="mt">🇰🇷 한국은행 기준금리</div>
      <div class="mv">2.75%</div>
      <div class="ms" style="color:var(--green)">인하 기조 유지. KRW 약세로 속도 조절.</div>
    </div>
    <div class="macro-item">
      <div class="mt">🏭 미국 ISM 제조업 PMI</div>
      <div class="mv">49.8</div>
      <div class="ms" style="color:var(--amber)">50 근접 경계선. 제조업 회복 기대 vs 유가 압박.</div>
    </div>
  </div>

  <div class="stitle">📌 포트폴리오 환율·원자재 노출도 매핑</div>
  <table>
    <thead><tr><th>구분</th><th>주요 종목</th><th>달러 강세 영향</th><th>유가 상승 영향</th></tr></thead>
    <tbody>
      <tr><td>수혜</td><td>알파벳, 엔비디아, 비자, KO, UNH, RKLB, IONQ, PEP</td><td class="up">원화 환산가치 ↑ (자연 헤지)</td><td class="dn">간접 비용 부담 (클라우드 전력비)</td></tr>
      <tr><td>중립</td><td>삼성전자, SK하이닉스, 삼성전기, 이수페타시스</td><td class="up">수출 환차익 일부</td><td class="dn">반도체 소재비 소폭 상승</td></tr>
      <tr><td>피해</td><td>현대차, 하이브, 에코프로비엠</td><td class="dn">원가 상승 → 마진 압박</td><td class="dn">물류비·원자재비 직접 영향</td></tr>
    </tbody>
  </table>

  <div class="ibox info">💡 현재 USD/KRW 1,500원 고환율은 미국 주식 비중이 40%에 달하는 이 포트폴리오에 <strong>자연 헤지</strong>로 작용 중. 이란 전쟁 종식·협상 타결 시 원화 강세 전환으로 환산 손실 발생 가능성 모니터링 필요.</div>
</div>

<!-- ===== 포트폴리오 현황 ===== -->
<div class="card">
  <div class="card-title">📌 포트폴리오 현황 (기준일: 2026.03.28)</div>
  <div class="pgrid">
    <div class="pitem"><div class="pn">삼성전자</div><div class="pv">28.5%</div><div class="ps">₩20,306,100</div><div class="pr ret-pos">수익률 +22.3%</div></div>
    <div class="pitem"><div class="pn">알파벳 A</div><div class="pv">14.8%</div><div class="ps">₩10,588,910</div><div class="pr ret-neg">수익률 -3.2%</div></div>
    <div class="pitem"><div class="pn">하이브 ⚠️</div><div class="pv" style="color:var(--amber)">10.8%</div><div class="ps">₩7,675,000</div><div class="pr ret-neg">수익률 -17.0%</div></div>
    <div class="pitem"><div class="pn">엔비디아</div><div class="pv">9.8%</div><div class="ps">₩7,005,991</div><div class="pr ret-neg">수익률 -5.8%</div></div>
    <div class="pitem"><div class="pn">현대차</div><div class="pv">7.6%</div><div class="ps">₩5,445,000</div><div class="pr ret-neg">수익률 -3.1%</div></div>
    <div class="pitem"><div class="pn">SK하이닉스</div><div class="pv">6.5%</div><div class="ps">₩4,610,000</div><div class="pr ret-neg">수익률 -2.3%</div></div>
    <div class="pitem"><div class="pn">에코프로비엠</div><div class="pv" style="color:var(--amber)">5.4%</div><div class="ps">₩3,847,500</div><div class="pr ret-neg">수익률 -10.7%</div></div>
    <div class="pitem"><div class="pn">삼성전기</div><div class="pv">4.9%</div><div class="ps">₩3,472,000</div><div class="pr ret-neg">수익률 -5.2%</div></div>
    <div class="pitem"><div class="pn">기타 9종</div><div class="pv">11.7%</div><div class="ps">~₩8,344,765</div><div class="pr ret-neg">이수페타시스 등</div></div>
  </div>
  <div class="ch-wrap"><canvas id="pieChart"></canvas></div>
</div>

<!-- ===== 목차 ===== -->
<div class="card">
  <div class="card-title">📋 종목별 분석 목차</div>
  <div class="toc">
    <div class="toc-item" onclick="go('s1')"><div class="toc-n">① 삼성전자</div><div class="toc-s">⭐ 8.5/10 · 28.5% · ₩179,700</div></div>
    <div class="toc-item" onclick="go('s2')"><div class="toc-n">② SK하이닉스</div><div class="toc-s">⭐ 8.5/10 · 6.5% · ₩922,000</div></div>
    <div class="toc-item" onclick="go('s3')"><div class="toc-n">③ 이수페타시스</div><div class="toc-s">⭐ 8.0/10 · 2.3% · ₩110,500</div></div>
    <div class="toc-item" onclick="go('s4')"><div class="toc-n">④ 알파벳 A</div><div class="toc-s">⭐ 8.0/10 · 14.8% · ~$275</div></div>
    <div class="toc-item" onclick="go('s5')"><div class="toc-n">⑤ 엔비디아</div><div class="toc-s">⭐ 7.5/10 · 9.8% · ~$168</div></div>
    <div class="toc-item" onclick="go('s6')"><div class="toc-n">⑥ 현대차</div><div class="toc-s">⭐ 7.0/10 · 7.6% · ₩495,000</div></div>
    <div class="toc-item" onclick="go('s7')"><div class="toc-n">⑦ 하이브 ⚠️</div><div class="toc-s">⭐ 6.5/10 · 10.8% · ₩307,000</div></div>
    <div class="toc-item" onclick="go('s8')"><div class="toc-n">⑧ 에코프로비엠</div><div class="toc-s">⭐ 4.5/10 · 5.4% · ₩202,500</div></div>
    <div class="toc-item" onclick="go('s9')"><div class="toc-n">⑨ 삼성전기</div><div class="toc-s">⭐ 6.0/10 · 4.9% · ₩434,000</div></div>
    <div class="toc-item" onclick="go('s10')"><div class="toc-n">⑩ 기타 종목</div><div class="toc-s">디아이씨·V·KO·UNH·RKLB·IONQ·PEP</div></div>
  </div>
</div>

<!-- ===== 종목별 심층 분석 ===== -->
<div class="card">
  <div class="card-title">🔍 종목별 심층 분석</div>

  <!-- 삼성전자 -->
  <div class="scard" id="c-s1">
    <div class="shdr" onclick="tog('s1')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">① 삼성전자</span><span class="sticker">KRX:005930</span><span class="tag tag-b">HBM · 반도체</span></div>
      <div class="smeta"><span class="sprice">₩179,700</span><span class="sweight">28.5%</span><span class="sbadge bg-high">⭐ 8.5/10</span><span class="ret-pos" style="font-size:12px">+22.3%</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s1">
      <div class="ibox ok">💡 컨센서스 목표주가 ₩239,873 대비 현재가 <strong>33.5% 할인</strong>. TurboQuant 쇼크로 3/26 -4.71% 급락했으나 애널리스트 35명 매수/1명 매도 의견 불변. 평단 ₩146,912 대비 <strong>+22.3% 수익 중</strong>.</div>
      <div class="alert-banner" style="background:linear-gradient(90deg,#1e3a8a,#1d4ed8);font-size:12px;">🔬 TurboQuant 해석: KV캐시(추론 메모리) 압축이지, 학습 메모리(HBM 핵심 수요)가 아님. 장기 수요 훼손 제한적. 과반응 판단.</div>
      <div class="stitle">📈 예상 EPS 2026~2028</div>
      <table><thead><tr><th>연도</th><th>EPS</th><th>YoY</th><th>핵심 동인</th></tr></thead><tbody>
        <tr><td>2026E</td><td>₩20,000~22,000</td><td class="up">+80~100%</td><td>HBM4 수주, 4Q25 영업이익 20.1조 분기 최대</td></tr>
        <tr><td>2027E</td><td>₩24,000~28,000</td><td class="up">+20~27%</td><td>NAND 가격 반등, 용인 클러스터 증설</td></tr>
        <tr><td>2028E</td><td>₩28,000~33,000</td><td class="up">+15~20%</td><td>메모리 슈퍼사이클 지속</td></tr>
      </tbody></table>
      <div class="stitle">💰 적정주가 시나리오 (2026E EPS 기준)</div>
      <table><thead><tr><th>시나리오</th><th>EPS</th><th>PER</th><th>적정주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>보수 (Bear)</td><td>₩20,000</td><td>12x</td><td>₩240,000</td><td class="up">+33.6%</td></tr>
        <tr><td>기본 (Base)</td><td>₩22,000</td><td>13x</td><td>₩286,000</td><td class="up">+59.2%</td></tr>
        <tr><td>낙관 (Bull)</td><td>₩25,000</td><td>15x</td><td>₩375,000</td><td class="up">+108.7%</td></tr>
      </tbody></table>
      <div class="stitle">🎯 증권사 목표주가 컨센서스</div>
      <table><thead><tr><th>증권사</th><th>목표주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>키움증권</td><td>₩260,000</td><td class="up">+44.7%</td></tr>
        <tr><td>KB증권</td><td>₩240,000</td><td class="up">+33.6%</td></tr>
        <tr><td>골드만삭스</td><td>₩260,000</td><td class="up">+44.7%</td></tr>
        <tr><td>컨센서스 평균 (35명)</td><td>₩239,873</td><td class="up">+33.5%</td></tr>
        <tr><td>최고 목표주가</td><td>₩340,000</td><td class="up">+89.2%</td></tr>
      </tbody></table>
      <div class="ibox ok">✅ FCF: 4Q25 영업이익 20.1조 분기 최대. 자사주 소각 18.5조 진행 중. 순현금 보유. ROE 20% 이상 회복 예상.</div>
      <div class="stitle">🗓 향후 3개월 투자 로드맵</div>
      <div class="timeline">
        <div class="tl-item green"><div class="tl-date">4월 말</div><div class="tl-text">1Q26 실적 발표 → 영업이익 20조+ 확인 시 주가 재평가 트리거</div></div>
        <div class="tl-item amber"><div class="tl-date">3~4월</div><div class="tl-text">TurboQuant 오픈소스 공개 (Q2 예정) → 반도체 추가 충격 가능성 잔존. 단기 변동성 구간</div></div>
        <div class="tl-item green"><div class="tl-date">5~6월</div><div class="tl-text">자사주 소각 완료 → 주당 가치 제고, 수급 개선</div></div>
      </div>
      <div class="ibox warn">⚠️ 단기 리스크: TurboQuant 추가 충격(오픈소스 공개 시), 外人 순매도 지속, 이란 전쟁 고유가. 펀더멘털 훼손 없음. 현 구간(₩175,000~180,000)은 분할 매수 고려 가능.</div>
      <div class="stitle">📊 비교군 (메모리 반도체)</div>
      <table><thead><tr><th>항목</th><th>삼성전자</th><th>SK하이닉스</th><th>마이크론 (MU)</th></tr></thead><tbody>
        <tr><td>시가총액</td><td>약 1,060조원</td><td>약 670조원</td><td>약 $120B</td></tr>
        <tr><td>HBM 점유율</td><td>27%</td><td>57%</td><td>21%</td></tr>
        <tr><td>컨센서스 목표 Upside</td><td class="up">+33.5%</td><td class="up">+36.2%</td><td>+10~20%</td></tr>
        <tr><td>투자 매력도</td><td class="up">8.5/10</td><td class="up">8.5/10</td><td>7.0/10</td></tr>
      </tbody></table>
    </div>
  </div>

  <!-- SK하이닉스 -->
  <div class="scard" id="c-s2">
    <div class="shdr" onclick="tog('s2')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">② SK하이닉스</span><span class="sticker">KRX:000660</span><span class="tag tag-b">HBM 1위</span></div>
      <div class="smeta"><span class="sprice">₩922,000</span><span class="sweight">6.5%</span><span class="sbadge bg-high">⭐ 8.5/10</span><span class="ret-neg" style="font-size:12px">-2.3%</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s2">
      <div class="ibox ok">🏆 HBM 시장 점유율 57%. 2025년 4Q 영업이익 19.2조원 분기 최대. 컨센서스 목표주가 ₩1,255,697 (+36.2%). 38명 중 36명 매수.</div>
      <div class="alert-banner" style="background:linear-gradient(90deg,#1e3a8a,#1d4ed8);font-size:12px;">🔬 TurboQuant 쇼크로 3/26 -6.23% 급락. 엔비디아 H100 GPU 공급에 TurboQuant 8배 성능 향상 → 오히려 더 많은 GPU·HBM 가동 촉진 가능. 중장기 수요 훼손 아님.</div>
      <div class="stitle">💰 증권사 목표주가</div>
      <table><thead><tr><th>증권사</th><th>목표주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>하나증권 (최신)</td><td>₩1,450,000</td><td class="up">+57.3%</td></tr>
        <tr><td>KB증권</td><td>₩1,200,000</td><td class="up">+30.2%</td></tr>
        <tr><td>맥쿼리</td><td>₩1,120,000</td><td class="up">+21.5%</td></tr>
        <tr><td>컨센서스 평균 (38명)</td><td>₩1,255,697</td><td class="up">+36.2%</td></tr>
        <tr><td>최고 목표주가</td><td>₩1,700,000</td><td class="up">+84.4%</td></tr>
      </tbody></table>
      <div class="stitle">📈 예상 EPS & 영업이익</div>
      <table><thead><tr><th>연도</th><th>영업이익</th><th>YoY</th></tr></thead><tbody>
        <tr><td>2025 연간</td><td>47.2조원</td><td class="up">+101% (달성)</td></tr>
        <tr><td>2026E</td><td>100조~158조원</td><td class="up">HBM4 + DRAM↑</td></tr>
      </tbody></table>
      <div class="stitle">💰 적정주가 시나리오</div>
      <table><thead><tr><th>시나리오</th><th>내용</th><th>적정주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>Bear</td><td>HBM 점유율 하락</td><td>₩900,000</td><td class="dn">-2.4%</td></tr>
        <tr><td>Base</td><td>컨센서스</td><td>₩1,255,697</td><td class="up">+36.2%</td></tr>
        <tr><td>Bull</td><td>HBM4 독점 지속</td><td>₩1,700,000</td><td class="up">+84.4%</td></tr>
      </tbody></table>
      <div class="ibox ok">✅ 순현금 3.8조원 전환. 자사주 1,530만주(12.2조) 소각 예정. HBM 솔드아웃. 용인 클러스터 2027년 준공.</div>
      <div class="ibox warn">⚠️ TurboQuant 쇼크(추론 메모리 효율화) + 삼성·마이크론의 HBM 추격 + 대중국 수출 규제. 현 구간(₩900,000~950,000)은 분할 매수 고려 구간.</div>
      <div class="stitle">🗓 3개월 로드맵</div>
      <div class="timeline">
        <div class="tl-item green"><div class="tl-date">4월 말</div><div class="tl-text">1Q26 실적 발표 → 분기 영업이익 20조+ 예상. 확인 시 강력 매수 신호</div></div>
        <div class="tl-item green"><div class="tl-date">5월</div><div class="tl-text">ICLR 2026 (4/23) TurboQuant 발표 후 충격 소화 기간. 수급 안정 기대</div></div>
        <div class="tl-item amber"><div class="tl-date">2026 하반기</div><div class="tl-text">PC·모바일 DRAM 사이클 전환 모니터링 필요</div></div>
      </div>
    </div>
  </div>

  <!-- 이수페타시스 -->
  <div class="scard" id="c-s3">
    <div class="shdr" onclick="tog('s3')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">③ 이수페타시스</span><span class="sticker">KRX:007660</span><span class="tag tag-p">AI인프라 · MLB기판</span></div>
      <div class="smeta"><span class="sprice">₩110,500</span><span class="sweight">2.3%</span><span class="sbadge bg-high">⭐ 8.0/10</span><span class="ret-neg" style="font-size:12px">-7.1%</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s3">
      <div class="ibox ok">💡 매출 약 <strong>50%가 Google TPU 공급망</strong>. 다층 MLB 기판 글로벌 핵심 제조사. 2026년 제5공장 조기 증설 확정. 현재가 ₩110,500 대비 컨센서스 목표 +41% 업사이드. 증권사 4곳 전원 매수·목표주가 상향.</div>
      <div class="stitle">🎯 증권사 목표주가 (2026년 3월)</div>
      <table><thead><tr><th>증권사</th><th>목표주가</th><th>Upside</th><th>코멘트</th></tr></thead><tbody>
        <tr><td>한국투자증권</td><td>₩180,000</td><td class="up">+62.9%</td><td>조기 증설 확정, MLB 수요 견조</td></tr>
        <tr><td>신한투자증권</td><td>₩160,000</td><td class="up">+44.8%</td><td>고다층 기판 수요 폭발, 영업이익 55% 성장</td></tr>
        <tr><td>SK증권</td><td>₩144,000</td><td class="up">+30.3%</td><td>하이브리드 기판 양산 본격화</td></tr>
        <tr><td>키움증권</td><td>₩140,000</td><td class="up">+26.7%</td><td>2026E 매출 1.4조원 돌파 예상</td></tr>
        <tr><td>컨센서스 평균</td><td>₩156,000</td><td class="up">+41.2%</td><td></td></tr>
      </tbody></table>
      <div class="stitle">📈 예상 실적 & EPS</div>
      <table><thead><tr><th>연도</th><th>매출</th><th>영업이익</th><th>YoY</th></tr></thead><tbody>
        <tr><td>2025A</td><td>약 9,500억</td><td>약 850억</td><td>AI 인프라 수주 급증</td></tr>
        <tr><td>2026E</td><td>1조 4,478억</td><td>약 1,320억</td><td class="up">+55%</td></tr>
        <tr><td>2027E</td><td>1조 8,000억</td><td>약 1,800억</td><td class="up">+35%+</td></tr>
      </tbody></table>
      <div class="stitle">💰 적정주가 시나리오</div>
      <table><thead><tr><th>시나리오</th><th>EPS</th><th>PER</th><th>적정주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>Bear</td><td>₩3,000</td><td>35x</td><td>₩105,000</td><td class="dn">-5%</td></tr>
        <tr><td>Base</td><td>₩3,500</td><td>40x</td><td>₩140,000</td><td class="up">+26.7%</td></tr>
        <tr><td>Bull (Google TPU 독점 지속)</td><td>₩4,200</td><td>45x</td><td>₩189,000</td><td class="up">+71.0%</td></tr>
      </tbody></table>
      <div class="ibox ok">✅ 제5공장 조기 증설 확정(2026 하반기 가동). 다층 매출 비중 31%→50%+ 예상. 구글 외 메타·아마존 다변화 진행 중. AI 인프라 투자 둔화에도 MLB 수요는 구조적 성장.</div>
      <div class="ibox warn">⚠️ 고객사 구글 의존도 50%+로 집중 리스크. TurboQuant 추론 효율화가 구글의 데이터센터 CapEx 조정으로 이어질 경우 수주 감소 가능성. 현재 비중(2.3%)이 낮아 비중 확대 검토 의미 있음.</div>
      <div class="stitle">🗓 골든타임 & 액션 플랜</div>
      <div class="timeline">
        <div class="tl-item green"><div class="tl-date">지금~4월</div><div class="tl-text">현재가 ₩110,500: Bear 적정가와 거의 동일. 하방 제한적 + 41% 업사이드. 분할 매수 최적 구간.</div></div>
        <div class="tl-item green"><div class="tl-date">2Q26</div><div class="tl-text">제5공장 증설 가동 확인 시 실적 레버리지 가속화</div></div>
        <div class="tl-item green"><div class="tl-date">2H26</div><div class="tl-text">2026E 매출 1.4조 달성 가시화 → ₩140,000~160,000 목표</div></div>
      </div>
    </div>
  </div>

  <!-- 알파벳 A -->
  <div class="scard" id="c-s4">
    <div class="shdr" onclick="tog('s4')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">④ 알파벳 A</span><span class="sticker">NASDAQ:GOOGL</span><span class="tag tag-b">AI·빅테크</span></div>
      <div class="smeta"><span class="sprice">~$275 (₩413,705)</span><span class="sweight">14.8%</span><span class="sbadge bg-high">⭐ 8.0/10</span><span class="ret-neg" style="font-size:12px">-3.2%</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s4">
      <div class="ibox ok">💡 TurboQuant <strong>발표 주체로서 오히려 수혜</strong>. Google Cloud 성장 + Gemini AI + 반독점 여건 개선 기대. 73명 애널리스트 목표주가 $375 (+36.3%). P/E 27~28배로 빅테크 중 합리적 수준.</div>
      <div class="ibox info">🔬 TurboQuant 전략적 의미: Google의 추론 인프라 비용을 대폭 절감 → Google Cloud 마진 확대 + 경쟁력 강화. 반도체 쇼크를 촉발했지만 알파벳 자체에는 긍정 이벤트.</div>
      <div class="stitle">📈 예상 EPS</div>
      <table><thead><tr><th>연도</th><th>EPS</th><th>YoY</th><th>핵심 동인</th></tr></thead><tbody>
        <tr><td>2026E</td><td>$11.80</td><td class="up">+9%</td><td>Cloud·AI 광고, TurboQuant 비용 절감</td></tr>
        <tr><td>2027E</td><td>$13.50</td><td class="up">+14%</td><td>기업용 AI Gemini 수익화 본격화</td></tr>
        <tr><td>2028E</td><td>$15.50</td><td class="up">+15%</td><td>AI 검색 광고 + 멀티모달 플랫폼</td></tr>
      </tbody></table>
      <div class="stitle">💰 적정주가</div>
      <table><thead><tr><th>시나리오</th><th>EPS</th><th>PER</th><th>적정주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>Bear</td><td>$11.80</td><td>28x</td><td>$330</td><td class="up">+20%</td></tr>
        <tr><td>Base</td><td>$11.80</td><td>32x</td><td>$378</td><td class="up">+37.5%</td></tr>
        <tr><td>Bull</td><td>$13.50</td><td>35x</td><td>$472</td><td class="up">+71.6%</td></tr>
      </tbody></table>
      <div class="ibox ok">✅ FCF 약 $70B. 순이익률 32%+. 자사주 매입 $70B 지속. 반독점 소송 최악 시나리오(검색 독점 해소) 반영 시 Cloud·YouTube 가치만으로도 현재가 지지.</div>
      <div class="ibox warn">⚠️ 미 법무부 반독점 소송(Google Search 독점), 유럽 GDPR 규제, 이란 전쟁발 광고비 감소 가능성. TurboQuant로 반도체 쇼크의 촉발자가 되어 단기 기술주 전반 약세 요인.</div>
    </div>
  </div>

  <!-- 엔비디아 -->
  <div class="scard" id="c-s5">
    <div class="shdr" onclick="tog('s5')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">⑤ 엔비디아</span><span class="sticker">NASDAQ:NVDA</span><span class="tag tag-b">AI GPU</span></div>
      <div class="smeta"><span class="sprice">~$168 (₩252,620)</span><span class="sweight">9.8%</span><span class="sbadge bg-mid">⭐ 7.5/10</span><span class="ret-neg" style="font-size:12px">-5.8%</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s5">
      <div class="ibox ok">💡 42명 애널리스트 목표주가 $273 (+62.5%). AI GPU 92% 독점. TurboQuant는 H100에서 8배 성능 향상 → 오히려 기존 Nvidia H100·A100 가치 증명. 장기 AI 수요 구조 훼손 없음.</div>
      <div class="stitle">📈 예상 EPS (회계연도 1월)</div>
      <table><thead><tr><th>회계연도</th><th>EPS</th><th>YoY</th></tr></thead><tbody>
        <tr><td>FY2026E (1월)</td><td>$4.78~5.80</td><td class="up">+50~65%</td></tr>
        <tr><td>FY2027E (1월)</td><td>$8.30</td><td class="up">+43%</td></tr>
        <tr><td>FY2028E (1월)</td><td>$9.50</td><td class="up">+14%</td></tr>
      </tbody></table>
      <div class="stitle">💰 적정주가</div>
      <table><thead><tr><th>시나리오</th><th>EPS</th><th>PER</th><th>적정주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>Bear</td><td>$4.78</td><td>35x</td><td>$167</td><td class="dn">-0.6% (지지선)</td></tr>
        <tr><td>Base</td><td>$8.30</td><td>35x</td><td>$290</td><td class="up">+72.6%</td></tr>
        <tr><td>Bull</td><td>$9.50</td><td>40x</td><td>$380</td><td class="up">+126%</td></tr>
      </tbody></table>
      <div class="ibox ok">✅ 순이익률 52%. 데이터센터 매출 $51.2B (Q3, +66% YoY). Blackwell GB200 수요 견조. TurboQuant가 H100 성능을 8배 향상시키므로 추가 채택 유인 상승 역설.</div>
      <div class="ibox warn">⚠️ 평단 대비 -5.8%로 소폭 손실 중. TurboQuant 추가 쇼크(ICLR 발표 전후), 미국-중국 반도체 수출 규제 강화, H200·Blackwell 수율 이슈 모니터링 필요.</div>
    </div>
  </div>

  <!-- 현대차 -->
  <div class="scard" id="c-s6">
    <div class="shdr" onclick="tog('s6')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">⑥ 현대차</span><span class="sticker">KRX:005380</span><span class="tag tag-b">완성차·로봇</span></div>
      <div class="smeta"><span class="sprice">₩495,000</span><span class="sweight">7.6%</span><span class="sbadge bg-mid">⭐ 7.0/10</span><span class="ret-neg" style="font-size:12px">-3.1%</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s6">
      <div class="ibox ok">💡 피지컬 AI 기업으로 재평가 진행 중. 보스턴 다이내믹스 아틀라스 2027 양산 목표. 목표주가 컨센서스 ₩602,000 (+21.6%). 분기 배당 ₩2,500.</div>
      <div class="stitle">💰 적정주가 시나리오</div>
      <table><thead><tr><th>시나리오</th><th>EPS</th><th>PER</th><th>적정주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>Bear</td><td>₩40,000</td><td>11x</td><td>₩440,000</td><td class="dn">-11.1%</td></tr>
        <tr><td>Base</td><td>₩43,883</td><td>14x</td><td>₩614,000</td><td class="up">+24.0%</td></tr>
        <tr><td>Bull (로봇 재평가)</td><td>₩48,000</td><td>17x</td><td>₩816,000</td><td class="up">+64.8%</td></tr>
      </tbody></table>
      <div class="ibox ok">✅ 2025년 매출 175조원(+8% YoY). 배당수익률 4%+. IRA 종료 영향 제한적(미국 현지 생산 조지아 공장).</div>
      <div class="ibox warn">⚠️ 팰리세이드 OTA 리콜(전동시트 결함) 진행 중. 미국 관세 불확실성(트럼프 2기 자동차관세). 이란 전쟁발 유가 상승 → 내연기관 수요 단기 부진. 아틀라스 2027년 양산 일정 지연 리스크.</div>
      <div class="stitle">🗓 3개월 핵심 이벤트</div>
      <div class="timeline">
        <div class="tl-item amber"><div class="tl-date">4~5월</div><div class="tl-text">팰리세이드 OTA 업데이트 완료 확인 → 리콜 비용 제한적 여부 판단</div></div>
        <div class="tl-item green"><div class="tl-date">2Q26</div><div class="tl-text">1Q26 실적 발표 → 미국 공장 실적 확인 및 전기차 전환 비용 가이던스</div></div>
        <div class="tl-item green"><div class="tl-date">2H26</div><div class="tl-text">아틀라스 양산 프로그램 추가 발표 → 피지컬 AI 밸류에이션 재평가 트리거</div></div>
      </div>
    </div>
  </div>

  <!-- 하이브 -->
  <div class="scard" id="c-s7">
    <div class="shdr" onclick="tog('s7')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">⑦ 하이브 ⚠️</span><span class="sticker">KRX:352820</span><span class="tag tag-p">K-Pop·엔터</span></div>
      <div class="smeta"><span class="sprice">₩307,000</span><span class="sweight" style="background:#fef3c7;color:var(--amber)">10.8%</span><span class="sbadge bg-low">⭐ 6.5/10</span><span class="ret-neg" style="font-size:12px">-17.0%</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s7">
      <div class="ibox danger">🚨 광화문 컴백 공연 (3/21) 관중 실망: 서울시 추산 4.8만명 (경찰 예측 26만 대비 크게 미달). 주가 ₩344,000 → ₩307,000 (-10.7%). 단, 이는 <strong>무료 야외 공연</strong> 기준 — 4월 9일 <strong>유료 스타디움 공연이 진짜 실적 시그널</strong>.</div>
      <div class="ibox ok">💡 26명 애널리스트 전원 매수. 컨센서스 목표주가 ₩453,885 (+47.8%). 2026E 영업이익 5,000억~5,800억원(전년비 +1,063%). BTS 월드투어 79회 × 6.5만명 = 약 280만명 유료 관객.</div>
      <div class="stitle">📈 실적 전망 (BTS 투어 레버리지)</div>
      <table><thead><tr><th>연도</th><th>매출</th><th>영업이익</th><th>EPS</th><th>YoY</th></tr></thead><tbody>
        <tr><td>2025 연간</td><td>2,684억</td><td>86억</td><td>~₩2,000</td><td class="dn">구조조정·일회성 비용 반영</td></tr>
        <tr><td>2026E</td><td>3,690~4,296억</td><td>5,000~5,800억</td><td>₩8,513~10,937</td><td class="up">+1,063% (턴어라운드)</td></tr>
        <tr><td>2027E</td><td>3,732억+</td><td>516억+</td><td>~₩10,000+</td><td class="up">+10~15%</td></tr>
      </tbody></table>
      <div class="stitle">🎯 증권사 목표주가</div>
      <table><thead><tr><th>증권사</th><th>목표주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>NH투자증권</td><td>₩500,000</td><td class="up">+62.9%</td></tr>
        <tr><td>SK증권 · IBK투자증권</td><td>₩480,000</td><td class="up">+56.4%</td></tr>
        <tr><td>iM증권</td><td>₩420,000</td><td class="up">+36.8%</td></tr>
        <tr><td>IBK투자증권 (최신)</td><td>₩420,000</td><td class="up">+36.8%</td></tr>
        <tr><td>컨센서스 평균 (26명)</td><td>₩453,885</td><td class="up">+47.8%</td></tr>
        <tr><td>최저 목표주가</td><td>₩380,000</td><td class="up">+23.8%</td></tr>
      </tbody></table>
      <div class="stitle">💰 PER 기반 밸류에이션</div>
      <table><thead><tr><th>시나리오</th><th>2026E EPS</th><th>PER</th><th>적정주가</th><th>Upside</th></tr></thead><tbody>
        <tr><td>Bear (관중 실망 반영)</td><td>₩8,513</td><td>36x</td><td>₩306,468</td><td class="up">거의 현재가 (지지선)</td></tr>
        <tr><td>Base (컨센서스)</td><td>₩8,835</td><td>45x</td><td>₩397,575</td><td class="up">+29.5%</td></tr>
        <tr><td>Bull (BTS 풀 모멘텀)</td><td>₩10,937</td><td>50x</td><td>₩546,850</td><td class="up">+78.1%</td></tr>
      </tbody></table>
      <div class="stitle">🗓 핵심 이벤트 타임라인</div>
      <div class="timeline">
        <div class="tl-item red"><div class="tl-date">3/27 Netflix 다큐 공개</div><div class="tl-text">BTS 'ARIRANG' 다큐멘터리 넷플릭스 공개. 글로벌 팬덤 재결집 확인 포인트.</div></div>
        <div class="tl-item amber"><div class="tl-date">4/9 고양 스타디움</div><div class="tl-text"><strong>⚡ 진짜 테스트</strong>: 유료 스타디움 공연. 매진 여부·실제 관객 규모로 투어 수익화 가능성 판단. → 매진 확인 시 매수 기회.</div></div>
        <div class="tl-item green"><div class="tl-date">4~6월</div><div class="tl-text">BTS 북미·유럽 투어 → 공연·MD 매출 본격 발생</div></div>
        <div class="tl-item green"><div class="tl-date">상반기 실적</div><div class="tl-text">1Q26 실적 발표: BTS 투어 매출 최초 반영 확인 → 목표주가 재산정 트리거</div></div>
      </div>
      <div class="ibox warn">⚠️ 현재 하이브 평단 ₩369,800 대비 현재가 ₩307,000으로 -17% 손실 중. 광화문 관중 미달 이슈가 진짜 유료 공연 수요를 훼손하는지 여부가 핵심 판단 기준. 4/9 공연 전까지는 비중 유지 권장. 손절 기준: ₩270,000 이하.</div>
    </div>
  </div>

  <!-- 에코프로비엠 -->
  <div class="scard" id="c-s8">
    <div class="shdr" onclick="tog('s8')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">⑧ 에코프로비엠</span><span class="sticker">KOSDAQ:247540</span><span class="tag tag-a">2차전지</span></div>
      <div class="smeta"><span class="sprice">₩202,500</span><span class="sweight" style="background:#fef3c7;color:var(--amber)">5.4%</span><span class="sbadge bg-bad">⭐ 4.5/10</span><span class="ret-neg" style="font-size:12px">-10.7%</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s8">
      <div class="ibox warn">⚠️ KB증권이 3/26 <strong>투자의견 매수·목표주가 ₩250,000 유지</strong>. 1Q26 실적 우려 대비 양호 전망(영업이익 93억, +310% QoQ). 그러나 구조적 EV 침체·IRA 종료·중국 LFP 압박은 여전. 평단 ₩226,811 대비 -10.7% 손실.</div>
      <div class="stitle">📊 핵심 지표</div>
      <table><thead><tr><th>지표</th><th>수치</th><th>평가</th></tr></thead><tbody>
        <tr><td>KB증권 목표주가</td><td>₩250,000</td><td class="up">현재가 대비 +23.5% (매수)</td></tr>
        <tr><td>1Q26 영업이익 예상</td><td>93억원</td><td class="up">우려 대비 양호 (QoQ +310%)</td></tr>
        <tr><td>1Q26 매출</td><td>5,475억원</td><td class="dn">YoY -13%</td></tr>
        <tr><td>북미향 출하</td><td>부진 지속</td><td class="dn">IRA 종료, 포드 EV 판매 감소</td></tr>
        <tr><td>유럽향</td><td>회복 중</td><td class="up">재고조정 마무리, 반등 예상</td></tr>
        <tr><td>탄산리튬 가격</td><td>+23.9% (12월 말比)</td><td class="up">양극재 원가 부담 완화 방향</td></tr>
      </tbody></table>
      <div class="ibox info">🔄 <strong>판단 업데이트</strong>: 이전 강력 매도 권고에서 <strong>조건부 보유로 완화</strong>. KB증권의 최신 매수 의견(3/26)과 1Q26 실적 예상 양호 감안. 단, 구조적 EV 회복 없이 장기 보유는 비효율. 1Q26 실적 확인 후 비중 조정 결정 권장.</div>
      <div class="ibox warn">⚠️ IRA 종료 → 북미 전기차 세금 공제 소멸. 중국 LFP 원가 압박 구조적 지속. 포드·현대차 EV 판매 부진. 장기적으로 NCM 하이니켈 양극재 수요 회복까지 시간 필요. 1Q26 실적 발표 후 가이던스에 따라 비중 재검토.</div>
    </div>
  </div>

  <!-- 삼성전기 -->
  <div class="scard" id="c-s9">
    <div class="shdr" onclick="tog('s9')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">⑨ 삼성전기</span><span class="sticker">KRX:009150</span><span class="tag tag-b">MLCC·AI기판</span></div>
      <div class="smeta"><span class="sprice">₩434,000</span><span class="sweight">4.9%</span><span class="sbadge bg-mid">⭐ 6.0/10</span><span class="ret-neg" style="font-size:12px">-5.2%</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s9">
      <div class="ibox info">💡 AI MLCC 슈퍼사이클 + FC-BGA 수주 확보. 2026년 영업이익 1.14조원 (+26%). 27명 전원 매수. 컨센서스 목표주가 ₩450,893.</div>
      <div class="ibox warn">⚠️ 현재가(₩434,000) 이미 컨센서스 목표가(₩450,893)에 근접. 실질 업사이드 +3.9%로 매우 제한적. 유리기판 양산 2027~2028년으로 단기 재평가 트리거 부재. 추가 매수보다 <strong>현 비중 유지</strong> 권장.</div>
    </div>
  </div>

  <!-- 기타 종목 -->
  <div class="scard" id="c-s10">
    <div class="shdr" onclick="tog('s10')">
      <div style="display:flex;align-items:center;gap:9px"><span class="sname">⑩ 기타 종목</span><span class="sticker">디아이씨 · V · KO · UNH · RKLB · IONQ · PEP · KODEX2차전지</span></div>
      <div class="smeta"><span class="sbadge bg-mid">다양</span><span class="tico">▼</span></div>
    </div>
    <div class="sbody" id="b-s10">
      <table>
        <thead><tr><th>종목</th><th>현재가(KRW)</th><th>수익률</th><th>매력도</th><th>한 줄 요약</th><th>권고</th></tr></thead>
        <tbody>
          <tr><td>이수페타시스 (007660)</td><td>₩110,500</td><td class="dn">-7.1%</td><td class="up">8.0/10</td><td>AI 인프라 MLB 핵심. 목표주가 컨센서스 +41%. 비중 확대 여지.</td><td class="up">비중 확대 검토</td></tr>
          <tr><td>디아이씨 (092200)</td><td>₩8,600</td><td class="dn">-22.5%</td><td class="dn">4.0/10</td><td>EV·로봇 감속기. 실적 뒷받침 부족. 큰 손실 중.</td><td class="dn">보유 최소화</td></tr>
          <tr><td>KODEX 2차전지 ETF</td><td>₩16,870</td><td class="dn">-11.3%</td><td class="dn">3.5/10</td><td>에코프로비엠과 섹터 이중 노출.</td><td class="dn">정리 검토</td></tr>
          <tr><td>비자 (V)</td><td>₩445,644</td><td class="dn">-3.0%</td><td class="up">6.5/10</td><td>결제 독점, 안정 FCF. 방어적 가치주.</td><td>유지</td></tr>
          <tr><td>코카콜라 (KO)</td><td>₩114,171</td><td class="up">+6.7%</td><td>6.0/10</td><td>방어주·배당. 유일한 수익 종목. 고유가·인플레 헤지.</td><td>유지</td></tr>
          <tr><td>UnitedHealth (UNH)</td><td>₩390,602</td><td class="dn" style="color:#dc2626;font-weight:800">-38.7% ⚠️</td><td class="dn">3.5/10</td><td>의료보험 손해율 급등 + 규제 강화. 포트폴리오 최대 손실. 보유 비중(0.5%) 다행히 소규모.</td><td class="dn">손절 검토</td></tr>
          <tr><td>로켓랩 (RKLB)</td><td>₩91,882</td><td class="dn">-25.6%</td><td>5.0/10</td><td>소형 위성 성장주. 고위험. 비중 0.4%.</td><td>소형 유지</td></tr>
          <tr><td>아이온큐 (IONQ)</td><td>₩41,485</td><td class="dn" style="color:#dc2626;font-weight:800">-38.8% ⚠️</td><td class="dn">3.5/10</td><td>양자컴퓨팅 투기. 비중 0.3%로 영향 미미하나 손실 큼.</td><td class="dn">손절 검토</td></tr>
          <tr><td>펩시코 (PEP)</td><td>₩230,784</td><td class="dn">-3.7%</td><td>5.5/10</td><td>방어주. 배당 견고. 포트폴리오 안전판. 비중 0.1%.</td><td>유지</td></tr>
        </tbody>
      </table>
    </div>
  </div>
</div>

<!-- ===== 관리 필요 종목 ===== -->
<div class="card">
  <div class="card-title">🚨 관리 필요 종목 — 즉시 액션 플랜</div>

  <div class="acard sell">
    <div class="atitle">UnitedHealth (UNH) <span class="atag">손절 검토</span></div>
    <p style="font-size:12px;color:var(--tx2)">비중 0.5% | 평단 ₩637,249 → 현재가 ₩390,602 | <strong style="color:var(--red)">손실 -38.7% (-₩247,000)</strong></p>
    <ul>
      <li>미국 의료보험 손해율 급등 + 민주당·공화당 양당 보험사 규제 논의</li>
      <li>의료 CEO 총격 사건 이후 사회적 반감 + 구조적 적자 리스크</li>
      <li>비중이 0.5%(약 ₩38만)로 영향은 미미. 관리 비용 대비 효율 낮음</li>
      <li>👉 소규모 포지션이므로 즉시 손절 후 예수금 보강 권장</li>
    </ul>
  </div>

  <div class="acard sell">
    <div class="atitle">아이온큐 (IONQ) <span class="atag">손절 검토</span></div>
    <p style="font-size:12px;color:var(--tx2)">비중 0.3% | 평단 ₩67,792 → 현재가 ₩41,485 | <strong style="color:var(--red)">손실 -38.8%</strong></p>
    <ul>
      <li>양자컴퓨팅 테마주로 비중 매우 작음(₩18만). 투기적 포지션</li>
      <li>비중 0.3%로 손실 절대금액 ₩11만원 수준. 실질적 포트폴리오 영향 없음</li>
      <li>👉 포트폴리오 단순화 차원에서 정리 권장</li>
    </ul>
  </div>

  <div class="acard warn2">
    <div class="atitle">KODEX 2차전지산업 ETF <span class="atag">정리 검토</span></div>
    <p style="font-size:12px;color:var(--tx2)">비중 0.5% | 손실 -11.3% | 에코프로비엠과 섹터 이중 노출</p>
    <ul>
      <li>에코프로비엠 보유 중 2차전지 ETF 추가 보유는 섹터 집중 위험</li>
      <li>비중(0.5%)과 금액(₩33만)이 작아 즉시 정리로 포트폴리오 단순화</li>
      <li>매도 후 예수금 보강</li>
    </ul>
  </div>

  <div class="acard warn2">
    <div class="atitle">에코프로비엠 (247540) <span class="atag">조건부 보유 → 실적 후 재검토</span></div>
    <p style="font-size:12px;color:var(--tx2)">비중 5.4% | 평단 ₩226,811 → 현재가 ₩202,500 | 손실 -10.7%</p>
    <ul>
      <li>KB증권 3/26 매수 의견·목표주가 ₩250,000 (+23.5%) — 이전 강력 매도에서 일부 완화</li>
      <li>1Q26 실적 (4월 발표) 우려 대비 양호 전망 (영업이익 93억, QoQ +310%)</li>
      <li>👉 1Q26 실적 발표 전 보유 유지. 가이던스 개선 시 홀드, 악화 시 비중 축소</li>
    </ul>
  </div>

  <div class="acard buy2">
    <div class="atitle">삼성전자 (005930) <span class="atag">현 비중 유지 — 분할 매수 지속</span></div>
    <p style="font-size:12px;color:var(--tx2)">비중 28.5% | 평단 ₩146,912 | <strong style="color:var(--green)">수익 +22.3%</strong> | 컨센서스 +33.5% 업사이드 잔존</p>
    <ul>
      <li>TurboQuant 쇼크는 단기 과반응. 펀더멘털 훼손 없음</li>
      <li>4월 말 1Q26 실적 발표 → 영업이익 20조+ 확인 시 강력 매수 신호</li>
      <li>예수금(₩858,503) + UNH/IONQ 정리 대금으로 ₩175,000~180,000 구간 분할 매수 검토</li>
    </ul>
  </div>

  <div class="acard hold">
    <div class="atitle">하이브 (352820) <span class="atag">4/9 공연 관찰 후 결정</span></div>
    <p style="font-size:12px;color:var(--tx2)">비중 10.8% | 평단 ₩369,800 | 손실 -17.0% | 컨센서스 목표주가 +47.8%</p>
    <ul>
      <li>광화문 무료 공연 4.8만명 실망은 <strong>유료 공연 수요와 무관</strong></li>
      <li>4월 9일 고양 스타디움 유료 공연 매진 여부가 핵심 판단 근거</li>
      <li>→ 매진 확인 시: 비중 유지 or 일부 확대 / 미달 시: 비중 축소 검토</li>
      <li>손절 기준선: ₩270,000 이하 (추가 -12%) 이탈 시</li>
    </ul>
  </div>

  <div class="acard buy2">
    <div class="atitle">이수페타시스 (007660) <span class="atag">비중 확대 검토</span></div>
    <p style="font-size:12px;color:var(--tx2)">현재 비중 2.3% (₩1,657,500) | 평단 ₩119,000 | 손실 -7.1% | 컨센서스 업사이드 +41%</p>
    <ul>
      <li>구글 TPU 공급망 50% + AI 데이터센터 MLB 기판 구조적 성장</li>
      <li>현재가 ₩110,500은 Bear 시나리오 적정가와 거의 일치 → 하방 제한적</li>
      <li>예수금 + 소형 포지션 정리 대금으로 ₩105,000~115,000 구간 비중 확대 검토</li>
    </ul>
  </div>
</div>

<!-- ===== 투자 매력도 점수 ===== -->
<div class="card">
  <div class="card-title">⭐ 투자 매력도 종합 점수 (10점 만점)</div>
  <div id="scores"></div>
  <div style="height:14px"></div>
  <div class="ch-wrap" style="height:360px"><canvas id="barChart"></canvas></div>
</div>

<!-- ===== 레이더 차트 ===== -->
<div class="card">
  <div class="card-title">🕸 핵심 보유 종목 5각형 분석</div>
  <div class="two-col">
    <div class="radar-wrap"><canvas id="radarChart1"></canvas></div>
    <div class="radar-wrap"><canvas id="radarChart2"></canvas></div>
  </div>
</div>

<!-- ===== 포트폴리오 종합 점검 ===== -->
<div class="card">
  <div class="card-title">📊 포트폴리오 종합 점검</div>
  <div class="stitle">📐 섹터 분산도 분석</div>
  <table>
    <thead><tr><th>섹터</th><th>주요 종목</th><th>비중</th><th>평가</th></tr></thead>
    <tbody>
      <tr><td>반도체·AI 하드웨어</td><td>삼성전자·SK하이닉스·엔비디아·이수페타시스·삼성전기</td><td class="up">56.4%</td><td class="dn">⚠️ 과집중. TurboQuant 쇼크 시 동조화 위험</td></tr>
      <tr><td>AI·빅테크</td><td>알파벳 A</td><td>14.8%</td><td class="up">적정. AI 수혜 업종</td></tr>
      <tr><td>K-Pop·엔터</td><td>하이브</td><td class="up">10.8%</td><td>적정. AI 섹터와 무상관</td></tr>
      <tr><td>완성차·로봇</td><td>현대차</td><td>7.6%</td><td class="up">적정. 피지컬 AI 다각화</td></tr>
      <tr><td>2차전지·소재</td><td>에코프로비엠·KODEX2차전지</td><td class="dn">5.9%</td><td class="dn">구조적 하강. 비중 축소 권장</td></tr>
      <tr><td>방어주·금융</td><td>V·KO·PEP</td><td class="up">4.4%</td><td class="up">안전판. 고유가·인플레 헤지</td></tr>
      <tr><td>미국 고위험</td><td>UNH·RKLB·IONQ</td><td class="dn">1.2%</td><td class="dn">손절 검토. 수익률 악화</td></tr>
      <tr><td>현금</td><td>예수금</td><td>1.2%</td><td class="dn">낮음. 기회 자산 부족</td></tr>
    </tbody>
  </table>

  <div class="stitle">📈 수익률 현황 요약</div>
  <table>
    <thead><tr><th>수익률 구간</th><th>종목</th><th>전략</th></tr></thead>
    <tbody>
      <tr><td><span class="up">+10% 이상</span></td><td>삼성전자 (+22.3%), 코카콜라 (+6.7%)</td><td>수익 실현 vs 장기 보유 판단. 삼성전자는 추가 업사이드 33% 잔존.</td></tr>
      <tr><td><span style="color:var(--tx2)">±5% 이내</span></td><td>SK하이닉스(-2.3%), 현대차(-3.1%), 알파벳(-3.2%), 비자(-3.0%), 엔비디아(-5.8%), 삼성전기(-5.2%)</td><td>이들 모두 업사이드가 충분. 보유 유지.</td></tr>
      <tr><td><span class="dn">-10~-20%</span></td><td>하이브(-17%), 에코프로비엠(-10.7%), KODEX2차전지(-11.3%)</td><td>하이브: 4/9 공연 관찰 후 결정. 에코프로: 실적 확인 후 재검토. ETF: 정리 검토.</td></tr>
      <tr><td><span class="dn" style="font-weight:800">-20% 이상</span></td><td>디아이씨(-22.5%), RKLB(-25.6%), UNH(-38.7%), IONQ(-38.8%)</td><td>UNH·IONQ: 손절 검토. RKLB·디아이씨: 소형이라 현상 유지.</td></tr>
    </tbody>
  </table>

  <div class="stitle">💡 3개월 포트폴리오 로드맵</div>
  <div class="timeline">
    <div class="tl-item red"><div class="tl-date">즉시</div><div class="tl-text">UNH·IONQ 손절 + KODEX 2차전지 정리 → 예수금 약 ₩95만원 확보</div></div>
    <div class="tl-item amber"><div class="tl-date">4월 9일</div><div class="tl-text">하이브 BTS 고양 스타디움 유료 공연 → 매진 여부 확인 후 비중 조정</div></div>
    <div class="tl-item green"><div class="tl-date">4월 말</div><div class="tl-text">삼성전자·SK하이닉스·에코프로비엠 1Q26 실적 발표 → 삼성전자 비중 확대 신호 확인</div></div>
    <div class="tl-item amber"><div class="tl-date">4~5월</div><div class="tl-text">ICLR 2026 (4/23) TurboQuant 공식 발표 → 반도체 2차 충격 모니터링. 구간 매수 기회 활용</div></div>
    <div class="tl-item green"><div class="tl-date">5~6월</div><div class="tl-text">이수페타시스 제5공장 증설 가동 시점 확인. 예수금으로 비중 확대 검토</div></div>
    <div class="tl-item green"><div class="tl-date">6월</div><div class="tl-text">Fed 6월 금리 인하 확률 ~47%. 인하 확인 시 성장주 전반 재평가 → 하이브·이수페타시스 모멘텀</div></div>
  </div>
</div>

<!-- ===== 면책 ===== -->
<div class="card" style="background:#fff8f0;border:1px solid #fde68a">
  <div class="card-title" style="color:var(--amber)">⚠️ 투자 유의사항</div>
  <p style="font-size:12px;color:var(--tx2);line-height:1.85">본 리포트는 AI 투자 비서가 공개된 시장 데이터(Investing.com, Yahoo Finance, 증권사 컨센서스)를 기반으로 자동 생성한 참고 자료입니다. 투자 권유 또는 금융 자문이 아니며, 최종 투자 결정은 반드시 본인의 판단과 책임 하에 이루어져야 합니다. 주식 투자는 원금 손실의 위험이 있으며, 과거 수익률이 미래 수익을 보장하지 않습니다.<br><br>
  <strong>생성일:</strong> 2026년 3월 28일 &nbsp;|&nbsp; <strong>생성 도구:</strong> Claude (Anthropic) AI 투자비서 v2.0</p>
</div>
</div>

<div class="footer">📊 AI 투자비서 자동 생성 리포트 | 2026.03.28 | 참고용 자료 — 투자 권유 아님</div>

<script>
// ===== 파이 차트 =====
new Chart(document.getElementById('pieChart'),{
  type:'doughnut',
  data:{
    labels:['삼성전자','알파벳A','하이브','엔비디아','현대차','SK하이닉스','에코프로비엠','삼성전기','이수페타시스','디아이씨','기타'],
    datasets:[{
      data:[28.5,14.8,10.8,9.8,7.6,6.5,5.4,4.9,2.3,2.3,7.1],
      backgroundColor:['#1a56db','#0d9f6e','#f59e0b','#76b900','#7c3aed','#0f766e','#dc2626','#0891b2','#8b5cf6','#9ca3af','#6b7280'],
      borderWidth:2,borderColor:'#fff'
    }]
  },
  options:{responsive:true,maintainAspectRatio:false,cutout:'62%',
    plugins:{legend:{position:'right',labels:{font:{size:11},padding:10}},
    tooltip:{callbacks:{label:ctx=>' '+ctx.label+': '+ctx.parsed.toFixed(1)+'%'}}}}
});

// ===== 점수 바 =====
const sd=[
  {n:'삼성전자',s:8.5,c:'#0d9f6e'},{n:'SK하이닉스',s:8.5,c:'#0d9f6e'},
  {n:'이수페타시스',s:8.0,c:'#0d9f6e'},{n:'알파벳 A',s:8.0,c:'#0d9f6e'},
  {n:'엔비디아',s:7.5,c:'#1a56db'},{n:'현대차',s:7.0,c:'#1a56db'},
  {n:'비자',s:6.5,c:'#1a56db'},{n:'하이브',s:6.5,c:'#b45309'},
  {n:'삼성전기',s:6.0,c:'#b45309'},{n:'코카콜라',s:6.0,c:'#b45309'},
  {n:'펩시코',s:5.5,c:'#b45309'},{n:'로켓랩',s:5.0,c:'#b45309'},
  {n:'에코프로비엠',s:4.5,c:'#dc2626'},{n:'디아이씨',s:4.0,c:'#dc2626'},
  {n:'KODEX2차전지',s:3.5,c:'#dc2626'},{n:'UNH',s:3.5,c:'#dc2626'},
  {n:'아이온큐',s:3.5,c:'#dc2626'}
];
const se=document.getElementById('scores');
sd.forEach(x=>{
  const w=(x.s/10*100).toFixed(0);
  se.innerHTML+=`<div class="sbar-wrap"><div class="sbar-lbl">${x.n}</div><div class="sbar-track"><div class="sbar-fill" style="width:${w}%;background:${x.c}">${x.s}</div></div><div class="sbar-num" style="color:${x.c}">${x.s}점</div></div>`;
});

// ===== 바 차트 =====
new Chart(document.getElementById('barChart'),{
  type:'bar',
  data:{labels:sd.map(x=>x.n),datasets:[{data:sd.map(x=>x.s),backgroundColor:sd.map(x=>x.c),borderRadius:4,borderWidth:0}]},
  options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,
    plugins:{legend:{display:false},tooltip:{callbacks:{label:ctx=>' '+ctx.parsed.x+'/10점'}}},
    scales:{x:{min:0,max:10,grid:{color:'rgba(0,0,0,.06)'},ticks:{color:'#6b7280',font:{size:11},callback:v=>v+'점'}},
    y:{grid:{display:false},ticks:{color:'#111827',font:{size:12}}}}}
});

// ===== 레이더 차트 1: 삼성전자 vs SK하이닉스 =====
const radarLabels=['밸류에이션','성장성','펀더멘털','수급·모멘텀','리스크 관리'];
new Chart(document.getElementById('radarChart1'),{
  type:'radar',
  data:{
    labels:radarLabels,
    datasets:[
      {label:'삼성전자',data:[8.5,8.5,8.5,7.5,7.5],borderColor:'#1a56db',backgroundColor:'rgba(26,86,219,0.15)',borderWidth:2,pointRadius:3},
      {label:'SK하이닉스',data:[8.0,9.0,9.0,7.0,7.5],borderColor:'#0d9f6e',backgroundColor:'rgba(13,159,110,0.15)',borderWidth:2,pointRadius:3},
      {label:'이수페타시스',data:[9.0,8.5,7.5,7.0,7.0],borderColor:'#7c3aed',backgroundColor:'rgba(124,58,237,0.10)',borderWidth:2,pointRadius:3}
    ]
  },
  options:{responsive:true,maintainAspectRatio:false,
    scales:{r:{min:0,max:10,ticks:{stepSize:2,font:{size:9}},pointLabels:{font:{size:11}}}},
    plugins:{legend:{position:'bottom',labels:{font:{size:11}}},title:{display:true,text:'반도체·AI 인프라 3인방'}}}
});

// ===== 레이더 차트 2: 알파벳 vs 하이브 vs 현대차 =====
new Chart(document.getElementById('radarChart2'),{
  type:'radar',
  data:{
    labels:radarLabels,
    datasets:[
      {label:'알파벳 A',data:[8.0,8.0,8.5,7.5,7.5],borderColor:'#1a56db',backgroundColor:'rgba(26,86,219,0.15)',borderWidth:2,pointRadius:3},
      {label:'하이브',data:[9.0,9.5,6.0,5.0,5.0],borderColor:'#f59e0b',backgroundColor:'rgba(245,158,11,0.15)',borderWidth:2,pointRadius:3},
      {label:'현대차',data:[7.5,7.0,7.5,6.5,6.5],borderColor:'#7c3aed',backgroundColor:'rgba(124,58,237,0.10)',borderWidth:2,pointRadius:3}
    ]
  },
  options:{responsive:true,maintainAspectRatio:false,
    scales:{r:{min:0,max:10,ticks:{stepSize:2,font:{size:9}},pointLabels:{font:{size:11}}}},
    plugins:{legend:{position:'bottom',labels:{font:{size:11}}},title:{display:true,text:'빅테크·엔터·모빌리티 비교'}}}
});

// ===== 아코디언 =====
function tog(id){
  const b=document.getElementById('b-'+id);
  const h=document.querySelector('#c-'+id+' .shdr');
  b.classList.toggle('open');h.classList.toggle('open');
}
function go(id){
  const el=document.getElementById('c-'+id);
  if(el){el.scrollIntoView({behavior:'smooth',block:'start'});const b=document.getElementById('b-'+id);const h=document.querySelector('#c-'+id+' .shdr');b.classList.add('open');h.classList.add('open');}
}
</script>
</body>
</html>
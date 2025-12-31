---
title: "trim 예제 for string"
img_path: /assets/images/VC++/
categories: [VC++]
tags: [VC++, STRING, TRIM]
---

string클래스에 trim하는 함수가 없어서 만들어 봤습니다.

* 2006.06.08 - 대소문자 변환 함수 추가
* 2007.3.9   - string 클래스는 비가상 소멸자를 가지므로 이것을 상속해서 사용할때 위험이 따르게 된다.\
그래서 클래스로 상속을 받는대신 네임스페이스로 묶음

```cpp
#ifndef __ISSTRING_H__
#define __ISSTRING_H__
 
#include <string>
#include <algorithm>
using namespace std;
 
namespace IsString
{

    void TrimLeft(string& str , const char* ch)
    {
        if(str.empty()) return;
        const std::string::size_type begin = str.find_first_not_of(ch);
        const std::string::size_type size  = str.size();

        if(std::string::npos == begin)
        {
                str.assign("");
        }
        else if( begin != 0)
        {
                str.assign(str.substr(begin, size));
        }
    }

    void TrimRight(string& str , const char* ch)
    {
        if(str.empty()) return;

        const std::string::size_type end   = str.find_last_not_of(ch) + 1;
        const std::string::size_type size  = str.size();

        if(0 == end)
        {
            str.assign("");
        }
        else if(end != size)
        {
            str.assign(str.substr(0 , end));
        }
    }

    void TrimWhiteSpace(string& str)
    {
        while((' ' == (str)[0]) || ('\t' == (str)[0]))
        {
            TrimLeft(str , " ");
            TrimRight(str , "\t");
        }

        while((' ' == (str)[str.length() - 1]) || ('\t' == (str)[str.length() - 1]))
        {
            TrimLeft(str , " ");
            TrimRight(str , "\t");
        }
    }

    void ReplaceOf(string& str , const string target, const string replacement)
    {
        string::size_type pos = 0, found;

        if (!target.empty())
        {
            string::size_type target_size = target.size();
            string::size_type replacement_size = replacement.size();
            while ((found = str.find (target, pos)) != string::npos)
            {
                    str.replace (found , target_size , replacement);
                    pos = found + replacement_size;
            }
        }
    }

    void ToUpper(string& str)
    {
        transform(str.begin() , str.end() , str.begin() , ::toupper);
    }

    void ToLower(string& str)
    {
        transform(str.begin() , str.end() , str.begin() , ::tolower);
    }
 };
 
 #endif
 ```
---
title: "CMFCColorButton"
comments: true 
img_path: /assets/images/MFC/
categories: [MFC]
tags: [MFC]
---

Palette를 사용하여 Color Pick Bar를 확장하는 것을 알아 보도록 하자.

말 그대로 선택할 색상들을 이용해 Palette를 생성한 다음 CMFCColorButton에 연결시키면 그걸로 끝~이다.

```cpp
// get color from table
const CString rPaletteFilePath = GetExecPath() + _T("Setting\\PALETTE.TBL");
ifstream ifile(rPaletteFilePath.operator LPCTSTR());
if(ifile.is_open())
{
    vector<string> oResult;
    string aLine;
    while(!ifile.eof())
    {
        getline(ifile , aLine);
        if(ifile.eof()) break;

        CTokenizer<CIsComma>::Tokenize(oResult , aLine , CIsComma());
        if(3 == oResult.size())
        {
            BYTE bR = atoi(oResult[0].c_str());
            BYTE bG = atoi(oResult[1].c_str());
            BYTE bB = atoi(oResult[2].c_str());

            m_RedEntry.push_back(bR);
            m_GreenEntry.push_back(bG);
            m_BlueEntry.push_back(bB);
        }
    }

    const UINT NUM_COLOURS = m_RedEntry.size();
    const UINT nSize = sizeof(LOGPALETTE) + sizeof(PALETTEENTRY)*NUM_COLOURS;

    LOGPALETTE *pLogPalette = (LOGPALETTE*)calloc(nSize , sizeof(BYTE));
    pLogPalette->palVersion = 0x300;
    pLogPalette->palNumEntries = NUM_COLOURS;
    for (int i = 0; i < NUM_COLOURS; i++)
    {
        //set the new color combination
        pLogPalette->palPalEntry[i].peRed = m_RedEntry[i];
        pLogPalette->palPalEntry[i].peGreen = m_GreenEntry[i];
        pLogPalette->palPalEntry[i].peBlue = m_BlueEntry[i];
        pLogPalette->palPalEntry[i].peFlags = 0;
    }
    m_Palette.CreatePalette(pLogPalette);
    free(pLogPalette);

    m_wndFDNColorButton.SetPalette(&m_Palette);
    m_wndMH_CBColorButton.SetPalette(&m_Palette);
```

위크 코드를 간단히 설명하면 색상에 대한 정보를 외부 파일에 두어 파일을 읽어서 팔레트를 생성한다.

코드부에 색상 정보를 두면 팔레트를 수정해야 할때마다 다시 컴파일을 해야 하므로 외부 파일에 두는 것이 편리하다.


그리고 나서 CMFCColorButton의 SetPalette 함수를 이용하여 팔레트와 버튼을 연결시켜주면 끝이다.

GetColor() 함수를 통해서 선택한 색상 정보를 가져올 수 있는데, 만일 팔레트에 동일한 색상이 있으면 사용자가 선택한 팔레트의 인덱스 번호를 가져올수가 없게 되는데...\
이 문제를 해결하는 방법을 생각해 봐야 겠다.

![](2010-04-13-1.jpg)

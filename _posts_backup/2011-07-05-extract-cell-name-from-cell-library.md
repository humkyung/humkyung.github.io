---
title: "extract cell name from cell library"
comments: true 
img_path: /assets/images/ustn/
categories: [USTN]
tags: [MDL, MSTN J]
---

```c
#include   
#include   
#include   
#include "w2Dgn.h" 
#include   
#include   

externvoidloadCellLibraryIfNeeded(char*libToLoad);
/*----------------------------------------------------------------------+  
| |  
| name GetCellNameFromCellLib |  
| |  
| author HumKyung.Baek |  
| |  
+----------------------------------------------------------------------*/  
Public intGetCellNameFromCellLib(char* pOutputTextFilePath , char* pstrCellLib) 
{ 
    ULong elemAddr[250], eofPos, filePos, actualPos, readPos; 
    intscanWords, status, i,j=0, numAddr, fileNum=CELL_LIB, offset; 
    charcellName[10], cellDescription[30], msg[132]; 
    Scanlist scanList; 
    MSElement cellElm; /*cell element descriptor */  
    FILE* fp = NULL; 

    if(fp = mdlTextFile_open(pOutputTextFilePath , TEXTFILE_WRITE)) 
    { 
        loadCellLibraryIfNeeded(pstrCellLib); 
        
        mdlScan_initScanlist (&scanList); 
        mdlScan_noRangeCheck (&scanList); 

        scanList.scantype = ELEMTYPE | NESTCELL; 
        scanList.extendedType = FILEPOS; 
        scanList.typmask[0] = TMSK0_CELL_LIB; 

        mdlScan_initialize (CELL_LIB, &scanList); 

        filePos = 0L; 
        actualPos = 0L; 
    
        /*--- loop through all cell elements in file --- */  
        do
        {
            scanWords = sizeof(elemAddr)/sizeof(short); 
            status = mdlScan_file(elemAddr, &scanWords, sizeof(elemAddr), &filePos); 
            numAddr = scanWords / sizeof(short);   
        
            for(i=0; i < NumAddr;++i)
            { 
                /*--- get cell descriptor --- */  
                if(mdlElement_read (&cellElm, CELL_LIB, elemAddr[i]) != SUCCESS) 
                    continue; 
                else  
                { 
                    inttype; 
                    
                    type = mdlElement_getType (&cellElm); 
                    if(type != 1) continue; 
                    
                    /*--- get cell name and description --- */ 
                    memset(cellName , 0, sizeof(char)*10); 
                    mdlCnv_fromR50ToAscii ( 6, (short*) &cellElm.cell_lib_hdr.name,cellName); 
                    //! trim right  
                    for(j = strlen(cellName) - 1;(j >= 0) && ((' '== cellName[j]) || ('\r'== cellName[j]) || ('\n'== cellName[j]));j--); 
                    cellName[j + 1] = '\0'; 66   67 memset(cellDescription , 0, sizeof(char)*30); 
                    mdlCnv_fromR50ToAscii (27, cellElm.cell_lib_hdr.descrip,cellDescription); 
                    //! trim right  
                    for(j = strlen(cellDescription) - 1;(j >= 0) && ((' '== cellDescription[j]) || ('\r'== cellDescription[j]) || ('\n'== cellDescription[j]));j--); 
                    cellDescription[j + 1] = '\0'; 

                    //! write cell name and description to output file.  
                    sprintf(msg , "%s^%s", cellName , cellDescription); 
                    mdlTextFile_putString(msg , fp , TEXTFILE_DEFAULT); 
                } 
            } 
        }while(status == BUFF_FULL); 

        mdlTextFile_close(fp); 
        
        returnSUCCESS; 
    } 

    returnFALSE; 
}
```

- 순서
1. Cell Library를 현재의 파일에 Attach합니다.(loadCellLibraryIfNeeded)
2. Scan List를 생성하여 CELL_LIB을 찾습니다.
3. 각 CELL_LIB의 Cell Name과 Description을 파일로 출력합니다.
 
주의.
파일을 읽거나 쓸때 mdlTextFile류의 함수를 사용하세요.\
mdl은 여러 operating system에 포팅이 되어 있기 때문에 \r,\n 등을 OS에 맞게 출력하는 기능이 있습니다.\
이것을 사용하는 것이 좋습니다.
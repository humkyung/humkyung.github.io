---
title: "Excel automation from C++ with MFC"
comments: true 
img_path: /assets/images/MFC/
categories: [MFC]
tags: [MFC, EXCEL]
---

After digging through the newsgroups for hours, decoding a ton of VB\
code for automating Excel, converting it to C++ using VC 6.0 and MFC,\
and enough hair pulling to make me bald, I thought I'd post this to\
save others the trouble. I created the following include file\
containing the constants used in most common arguments to the Excel\
functions for searching, copying, sorting, etc. and a sample mfc\
program segment that demonstrates their use.

Merry Christmas,

Bob

```cpp
/* File: xlConstants.h

*******************************************
/ Constants used in Excel automation from
/ Visual C++
/
/ Courtesy of Bob Ray -- 2003
/
/ Note: The values of additional xl constants can be
/ found by running Excel and selecting
/ Tools | Macro | Visual Basic Editor.
/
/ Press F2 to get to the Object Browser.
/ Type the name of the constant in the search window.
/ Find the constant and select it. Look at the lower
/ left of the window to get the value and add
/ it to this list of defines.

/ You will also need to #include "excel9.h" which is
/ created on command by Visual Studio.
/ Note: If you are using "excel8.h" or earlier
/ some of the Excel functions take a different
/ number of arguments

********************************************/


// optional argument for default or ignored parameters
// (Excel uses the value used the last time the function
/ was called).

#define vOpt COleVariant((long) DISP_E_PARAMNOTFOUND, VT_ERROR)


// *********** Search Constants for range.find() ***********

// Example:
/* range.find(What, After, LookIn, LookAt, SearchOrder,
SearchDirection, MatchCase, MatchByte)*/

// What takes a COleVariant
// e.g. COleVariant("FindThisString") or COleVariant(2314)


// After
// use vOpt




//LookIn

#define xlComments COleVariant((long) -4144)
#define xlFormulas COleVariant((long) -4123) // will find value in
any cell
#define xlValues COleVariant((long) -4163) // ignores hidden cells

//LookAt

#define xlWhole COleVariant((long) 1) // whole word search
#define xlPart COleVariant((long) 2) // partial word search

//SearchOrder (vOpt works here)

#define xlByRows COleVariant((long) 1)
#define xlByColumns COleVariant((long) 2)

//SearchDirection (required but usually has no effect)

#define xlNext (long) 1
#define xlPrev (long) 2

// MatchCase

#define xlMatchCase COleVariant((long) 1)
#define xlIgnoreCase COleVariant((long) 0)

// MatchByte

// ignored, use vOpt


// *********** Insert / delete constants ***********
// These tell Excel which way to shift cells after the action is
performed

//vOpt works here

#define xlRight COleVariant((long) -4161)
#define xlLeft COleVariant((long) -4159)
#define xlUp COleVariant((long) -4162)
#define xlDown COleVariant((long) -4121)
#define xlGuess COleVariant((long) 0)


// *********** Sort constants ***********

/* range.Sort(Key1, Key1Order, Key2, SortType, Key2Order, Key3,
Key3Order,Header,CustomOrder,MatchCase,Orientation,SortMethod); */

// For argument 1 (key1), use the following:

// VARIANT key1; // these lines set up first arg (key1) to sort
function
// V_VT(&key1) = VT_DISPATCH;
// V_DISPATCH(&key1) = objSheet.GetRange(COleVariant(buff),
COleVariant(buff));

// For key2 and key3, use the above or use vOpt if you don't need
them.


// Sort type (used when sorting pivot tables)

#define xlSortValues (long) 1
#define xlSortLabels (long) 2

// Sort order (Note: required but ignored for key2 and key3 if they
are vOpt)

#define xlAscending (long) 1
#define xlDescending (long) 2

// Header (Tells sort to leave first row of range alone when sorting)

#define xlHeader (long) 1
#define xlNoHeader (long) 2
// xlGuess defined above (long) 0

// CustomOrder

// Use vOpt

// Match Case
// Use MatchCase and IgnoreCase defined above,
// although they appear to have no effect here

// Sort Orientation
// (note: don't use xlByRows or xlByColumns here -- they're backwards)

#define xlTopToBottom (long) 1
#define xlLeftToRight (long) 2

//Sort Method

#define xlPinYin (long) 1 // this is the default
#define xlStroke (long) 2

// End of include file excel9.h


***************

Here's some MFC C++ code that opens Excel gets the number of rows and
columns, searches for a name, inserts a row, sets its value and sorts
the entire spreadsheet.

***************

void CAutoProjectDlg::OnRun()
{


// operates on spreadsheet c:\test.xls, a gradebook.
// code Searches for a name,
// adds a student,
// and then sorts the sheet.

// sheet has the following format:

// A B C D E F
// 1 IdNum Name Test1 Test2 Total Grade
// 2 143564 Adams
// 3 324534 Jones
// 4 323456 Wilson

// note: Total and Grade columns contain formulas


_Application app;
_Workbook objBook;
Workbooks objBooks;
Worksheets objSheets;
_Worksheet objSheet;
Range range;


// Start Excel and get Application object...

if(!app.CreateDispatch("Excel.Application"))
{
AfxMessageBox("Couldn't start Excel.");
return;
}

if(!UpdateData(TRUE)) {
AfxMessageBox("Can't Update");
return;
}


objBooks = app.GetWorkbooks();

CString name(_T("C:\\Test.xls"));

objBook = objBooks.Open(name,
vOpt, vOpt, vOpt, vOpt, vOpt, vOpt,
vOpt, vOpt, vOpt, vOpt, vOpt, vOpt);

objSheets = objBook.GetWorksheets();

// get sheet 1 of workbook
objSheet = objSheets.GetItem(COleVariant((short)1));

objSheet.Activate();



// This section gets the number of rows and columns
// in case we're curious

Range objTotal, objCols, objRows;


objTotal.AttachDispatch(objSheet.GetUsedRange());
objCols.AttachDispatch(objTotal.GetColumns());
objRows.AttachDispatch(objTotal.GetRows());

int NumRows = objRows.GetCount();
int NumCols = objCols.GetCount();

char buff[44];

//sprintf(buff,"Cols: %d",NumCols);
//AfxMessageBox(buff);

//sprintf(buff,"Rows: %d",NumRows);
//AfxMessageBox(buff);


// This section searches the second column for the string "TestString"


range = objSheet.GetRange(COleVariant("B2"),COleVariant("B60"));



if ( range.Find(COleVariant("Jones"), vOpt, xlFormulas, xlPart,
xlByRows, xlNext,xlIgnoreCase,vOpt) ){
AfxMessageBox("Found");
} else {
AfxMessageBox("Not Found");
}

// Now we'll insert a blank row just below the header row.

range = objSheet.GetRange(COleVariant("A2"),COleVariant("Z2"));

range.Insert(vOpt);

// Now we'll copy data from row 65 into the inserted row so
// it will contain the formulas.


Range src, dest;

src = objSheet.GetRange(COleVariant("A65"),COleVariant("Z65"));
dest= objSheet.GetRange(COleVariant("A2"),COleVariant("Z2"));

dest.SetValue(src.GetValue());

// Now that the inserted row has all the proper formulas, we'll set
// the data in cells A2 and D2.
// Note: m_ID and m_Name are variables set elsewhere in a dialog box.

//Set value of A2

range = objSheet.GetRange(COleVariant("A2"),COleVariant("A2"));
CString s;

// m_ID is a number we're storing as a string so we put a single
// quote in front of it
s.Format("'%s",m_ID);
range.SetValue(COleVariant(s));

//Set value of B2 (m_Name is already a string)
range = objSheet.GetRange(COleVariant("B2"),COleVariant("B2"));
range.SetValue(COleVariant(m_Name));

// Now we sort the entire sheet (leaving the header row untouched)

sprintf(buff,"B1"); // set column B as the key to sort on

VARIANT key1; // these lines set up first arg (key1) to sort
function
V_VT(&key1) = VT_DISPATCH;
V_DISPATCH(&key1) = objSheet.GetRange(COleVariant(buff),
COleVariant(buff));


range = objSheet.GetRange(COleVariant("A1"),COleVariant("Z70"));
range.Sort(key1, xlAscending, vOpt, vOpt, xlAscending, vOpt,
xlAscending,xlHeader,vOpt,xlIgnoreCase,xlTopToBottom,xlPinYin);

// Let the user see our work and
// decide when to close the spreadsheet.

app.SetVisible(TRUE);
app.SetUserControl(TRUE);

}

// End of C++ code segment
```

Hope this helps someone,\
Bob
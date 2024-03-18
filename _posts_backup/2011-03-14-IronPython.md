---
title: "IronPython"
comments: true 
img_path: /assets/images/Python/
categories: [Python]
tags: [Python]
---

아래 글에서 Python.NET을 사용하기로 했는데,

PythonEngine.Execute를 호출했을때 리턴 값을 받지 못하는 문제가 발생했습니다.

항상 null을 리턴하는 것이었습니다.

그래서 어쩔수 없이 다른 방법을 찾아야 했는데, 그 대안책이 IronPython입니다.

IronPython을 잠시 사용해 본 느낌은 C#과의 결합이 아주 잘 되어있다는 것입니다.

C#에서 IronPython의 자료형을 그대로 사용할수 있고,

C#에서 IronPython에 변수를 넘겨 줄때에도 아무런 변환없이 C#의 자료형을 사용할수 있습니다.

아래 파일을 참조합니다.

![](2011-03-14-1.png)
 

예제 코드
```c#
 using IronPython.Hosting;
 using IronPython.Runtime;
 using Microsoft.Scripting;
 using Microsoft.Scripting.Hosting;
 
  public partial class SpoolListForm : DocumentModuleBase
 {
         private ScriptEngine oPyEngine = Python.CreateEngine();

         /// <summary>
         /// 
         /// </summary>
         /// <param name="sender"></param>
         /// <param name="e"></param>
         private void toolStripButtonQuery_Click(object sender, EventArgs e)
         {
                 ///
                 /// do something
                 /// 
                 QueryResultDataSet oQueryResultDataSet = new QueryResultDataSet();
                 ScriptScope oScriptScope = oPyEngine.CreateScope();
                 oScriptScope.SetVariable("DataSet", oQueryResultDataSet);
 
                 Dictionary<string, string> oOP = new Dictionary<string, string>();
                 oOP.Add("SCHEDULE", "10");
                 oScriptScope.SetVariable("OP", oOP);
 
                 Dictionary<string,string> oMLS = new Dictionary<string,string>();
                 oMLS.Add("MAIN_SCHEDULE", "7");
                 oScriptScope.SetVariable("MLS", oMLS);
                 for (int i = 0; i < 1; ++i)
                 {
                         foreach (CSQLFile.Field oField in sqlFile.Fields)
                         {
                                 if (string.Empty != oField.Value)
                                 {
                                         oScriptScope.SetVariable("PREFIX", "C65");              //! set global variable
                                         oScriptScope.SetVariable("PACKAGE_SYSTEM_NO", "S1");    //! set global variable
                                         oScriptScope.SetVariable("PIECE_MARK_NO", "1");         //! set global variable
                                         string sResult = string.Empty;
                                         try
                                         {
                                                 object oResult = oPyEngine.Execute(oField.Value, oScriptScope);
                                                 sResult = oResult.ToString();
                                         }
                                         catch (Exception ex)
                                         {
                                                 Framework.MessageCenter.ShowMessage(ex);
                                         }
                                 }
                         }
                 }
         }
 }
 ```

C# + IronPython은 정말 궁합이 잘 맞는다는 느낌입니다.
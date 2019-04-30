---
title: Te.exe 命令选项
description: Te.exe 命令选项
ms.assetid: E9A9292D-FA30-410d-9322-BD0F321314F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc6d04e11e82734dd00eac0ed24269f8d93fae5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374039"
---
# <a name="teexe-command-options"></a>Te.exe 命令选项


-   [使用情况](#usage)
-   [选择/执行命令](#selectionexecutioncommands)
-   [记录器设置](#loggersettings)
-   [调试设置](#debugsettings)
-   [测试模式](#testmodes)

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


**te.exe** &lt;[测试\_二进制文件](#testbinaries)&gt; \[ [/appendWttLogging](#appendwttlogging) \] \[ [/breakOnCreate](#breakoncreate) \] \[ [/breakOnError](#breakonerror) \] \[ [/breakOnInvoke](#breakoninvoke) \] \[ [/coloredConsoleOutput](#coloredconsoleoutput) \] \[ [/console:flushWrites](#console-option) \] \[ /console:position =&lt;x，y&gt; \] \[ /console:size =&lt;x，y&gt; \] \[ /console： 最顶层\] [ \[/defaultAppDomain\]](#defaultappdomain) \[ [/disableConsoleLogging](#disableconsolelogging) \] \[ [/disableTimeouts](#disabletimeouts) \] \[ [/dpiaware](#dpiaware) \] \[ [/enableWttLogging](#enablewttlogging) \] \[ [/inproc](#inproc) \] \[ [/isolationLevel](#isolationlevel) \] \[ [/labMode](#labmode) \] \[ [/list](#list) \] \[ [/listProperties](#listproperties) \] \[ [/logFile:&lt;名称&gt;](#logfile) \] \[ [/logOutput:&lt;模式&gt;](#logoutput) \] \[ [/miniDumpOnCrash](#minidumponcrash) \] \[ [/miniDumpOnError](#minidumponerror) \] \[ [/name:&lt;testname&gt; ](#name) \] \[ [/outputFolder:&lt;folderName&gt; ](#outputfolder) \] \[ [/p:&lt;ParamName&gt;=&lt;ParamValue&gt; ](#p) \]\[<span class= class=""></span class=>&gt;](#wttdevicestringsuffix)\]

## <a name="span-idselectionexecutioncommandsspanspan-idselectionexecutioncommandsspanspan-idselectionexecutioncommandsspanselectionexecution-commands"></a><span id="SelectionExecutionCommands"></span><span id="selectionexecutioncommands"></span><span id="SELECTIONEXECUTIONCOMMANDS"></span>选择/执行命令


### <a name="testbinaries"></a>测试\_二进制文件

指定要执行的一个或多个测试文件 （由空格分隔）。 支持使用通配符。

<span id="te.exe_test1.dll"></span><span id="TE.EXE_TEST1.DLL"></span>te.exe test1.dll  
**解释：** Test1.dll 中运行所有测试。

<span id="te.exe_test1.dll_test2.dll_test3.dll"></span><span id="TE.EXE_TEST1.DLL_TEST2.DLL_TEST3.DLL"></span>te.exe test1.dll test2.dll test3.dll  
**解释：** Test1.dll、 test2.dll 和 test3.dll 中运行所有测试。

<span id="te.exe__.dll"></span><span id="TE.EXE__.DLL"></span>te.exe \*.dll  
**解释：** 在当前目录中的所有 dll 中运行所有测试。

### <a name="span-idcoloredconsoleoutputspanspan-idcoloredconsoleoutputspanspan-idcoloredconsoleoutputspancoloredconsoleoutputlttruefalsegt"></a><span id="coloredConsoleOutput"></span><span id="coloredconsoleoutput"></span><span id="COLOREDCONSOLEOUTPUT"></span>/coloredConsoleOutput:&lt;true/false&gt;

指定 TAEF 应输出彩色的控制台文本。 默认值为 true。 如果设置为 false，TAEF 将输出与默认控制台颜色的所有文本。

**te.exe test1.dll /coloredConsoleOutput:false**

### <a name="span-idconsoleoptionspanspan-idconsoleoptionspanconsoleltoptionnamegtltvaluegt"></a><span id="console_option"></span><span id="CONSOLE_OPTION"></span>/console:&lt;optionName&gt;=&lt;value&gt;

提供用于配置 TE 的使用控制台的选项。 你可使用以下选项：

<span id="console-option"></span>**/console:flushWrites**  
会导致刷新后的每个行是编写-有用时 TE.exe 的输出已被重定向的控制台输出。

<span id="_console_position__x_y___current__"></span><span id="_CONSOLE_POSITION__X_Y___CURRENT__"></span>**/console:position =\[x，y | 当前 \]**  
设置控制台窗口相对于主监视器的角 （以像素为单位） 的位置。 使用值**当前**指定应存储和从重新启动恢复时使用当前控制台的位置。

<span id="_console_size____x_y____current__"></span><span id="_CONSOLE_SIZE____X_Y____CURRENT__"></span>**/console:size=\[ &lt;x,y&gt; | current \]**  
设置 （在字符维度） 的控制台窗口的大小。 将增加屏幕缓冲区大小，以匹配窗口如有必要的大小。 使用值**当前**指定应存储和从重新启动恢复时使用当前控制台大小。

<span id="_console_topmost"></span><span id="_CONSOLE_TOPMOST"></span>**/console:topmost**  
保留的执行持续时间内运行 te.exe 最顶端桌面的 z 顺序中的控制台。

### <a name="span-iddpiawarespanspan-iddpiawarespandpiaware"></a><span id="dpiaware"></span><span id="DPIAWARE"></span>/dpiaware

在进程中执行的测试标记为 DPI 感知，请参阅[高 DPI](https://msdn.microsoft.com/library/windows/desktop/dd464646)。 这也可以设置通过元数据 ("DpiAware")。

### <a name="span-idinprocspanspan-idinprocspaninproc"></a><span id="inproc"></span><span id="INPROC"></span>/inproc

执行在 TE.exe 进程本身而不是测试内的所有测试。ProcessHost.exe。

<span id="te.exe_test1.dll__inproc"></span><span id="TE.EXE_TEST1.DLL__INPROC"></span>te.exe test1.dll /inproc  
**注意：** TE 仅支持一次执行一个测试 dll 时使用 */inproc*设置。

### <a name="span-idisolationlevelspanspan-idisolationlevelspanspan-idisolationlevelspanisolationlevelltlevelgt"></a><span id="isolationLevel"></span><span id="isolationlevel"></span><span id="ISOLATIONLEVEL"></span>/isolationLevel:&lt;级别&gt;

指定的最小执行 TAEF 测试时要使用的隔离级别。 如果此值与指定为元数据的隔离级别冲突，值将成为具有紧密的作用域的隔离级别。 请参阅[测试隔离](test-isolation.md)的更多详细信息。

**te.exe test1.dll /isolationLevel:Class**

### <a name="span-idlabmodespanspan-idlabmodespanspan-idlabmodespanlabmode"></a><span id="labMode"></span><span id="labmode"></span><span id="LABMODE"></span>/labMode

执行测试，并删除潜在阻止的用户界面 （例如，Windows 错误报告对话框上崩溃测试）。

### <a name="span-idlistspanspan-idlistspanlist"></a><span id="list"></span><span id="LIST"></span>/list

列出所有的名称[测试\_二进制文件](#testbinaries)、 类和其中的方法。 如果指定选择条件，则会列出那些符合条件的的名称。

```cpp
 te.exe test1.dll test2.dll /list

 WEX::UnitTests::Test1
  WEX::UnitTests::Test1::Example1
  WEX::UnitTests::Test1::Example2
  WEX::UnitTests::Test1::Example3

 WEX::UnitTests::Test2
  WEX::UnitTests::Test2::Example1
  WEX::UnitTests::Test2::Example2
  WEX::UnitTests::Test2::Example3
```

```cpp
 te.exe test1.dll test2.dll /select:@name='*Example2*' /list

 WEX::UnitTests::Test1
  WEX::UnitTests::Test1::Example2

 WEX: :UnitTests::Test2
  WEX::UnitTests::Test2::Example2
```

### <a name="span-idlistpropertiesspanspan-idlistpropertiesspanspan-idlistpropertiesspanlistproperties"></a><span id="listProperties"></span><span id="listproperties"></span><span id="LISTPROPERTIES"></span>/listProperties

列出了名称和属性的所有测试\_二进制文件的类和方法中的以及设置和清除函数名，如果可用。 如果指定选择条件，则会列出那些符合条件的的名称。

```cpp
 te.exe test1.dll test2.dll /listProperties

 WEX::UnitTests::Test1
  WEX::UnitTests::Test1::Example1
   Setup: Test1Setup
   Teardown: Test1Teardown
   Property[ThreadingModel] = MTA
  WEX::UnitTests::Test1::Example2
   Setup: Test1Setup
   Teardown: Test1Teardown
   Property[ThreadingModel] = STA
  WEX::UnitTests::Test1::Example3
   Setup: Test1Setup
   Teardown: Test1Teardown
   Property[ThreadingModel] = STA

 WEX::UnitTests::Test2
  WEX::UnitTests::Test2::Example1
   Property[ThreadingModel] = MTA
  WEX::UnitTests::Test2::Example2
   Property[ThreadingModel] = STA
  WEX::UnitTests::Test2::Example3
   Property[ThreadingModel] = MTA
```

```cpp
 te.exe test1.dll test2.dll /select:@name='*Example2*' /listProperties

 WEX::UnitTests::Test1
  WEX::UnitTests::Test1::Example2
   Setup: Test1Setup
   Teardown: Test1Teardown
   Property[ThreadingModel] = STA

 WEX::UnitTests::Test2
  WEX::UnitTests::Test2::Example2
   Property[ThreadingModel] = STA
```

### <a name="span-idnamespanspan-idnamespannamelttestnamegt"></a><span id="name"></span><span id="NAME"></span>/name:&lt;testname&gt;

测试名称基于所选内容是为轻松的替代方法"/select:@Name='&lt;testname&gt;'"。 &lt;Testname&gt;仍可以包含通配符 ("\*"和"？")，但不是能包含单引号内。 如果 /select 和 /name 同时指定在命令提示符处，则/选择查询优先和 /name 将被忽略。

<span id="te.exe_test1.dll__name__TestToLower"></span><span id="te.exe_test1.dll__name__testtolower"></span><span id="TE.EXE_TEST1.DLL__NAME__TESTTOLOWER"></span>te.exe test1.dll /name:\*TestToLower  
**解释：** 运行所有测试方法名称与 TestToLower 的结束位置 test1.dll。 可以使用作为选择条件表示相同/select:@Name=\*TestToLower。

<span id="te.exe_test1.dll__name__StringTest_"></span><span id="te.exe_test1.dll__name__stringtest_"></span><span id="TE.EXE_TEST1.DLL__NAME__STRINGTEST_"></span>te.exe test1.dll /name:\*StringTest\*  
**解释：** 运行 test1.dll 中的所有测试，其中包含短语 StringTest 命名空间、 类或方法名称中。

### <a name="span-idoutputfolderspanspan-idoutputfolderspanspan-idoutputfolderspanoutputfolderltfoldernamegt"></a><span id="outputFolder"></span><span id="outputfolder"></span><span id="OUTPUTFOLDER"></span>/outputFolder:&lt;folderName&gt;

指定用于放置生成的所有文件的文件夹。 默认值为当前目录。 可以使用环境变量，例如：

**te.exe test1.dll /outputFolder:%TEMP%\\MyOutput**

### <a name="span-idpspanspan-idpspanpltparamnamegtltparamvaluegt"></a><span id="p"></span><span id="P"></span>/p:&lt;ParamName&gt;=&lt;ParamValue&gt;

定义与参数名称的运行时参数 = ParamName 和参数值 = 参数值。 这些参数是可从测试方法或安装程序/清理方法访问。

**te.exe test1.dll /p:x=5 /p:myParm=cool**

您可以获取 x 作为一个多个测试代码中支持的类型。 例如，这里您可以看到我们为 int 和 WEX::Common::String 检索：

```cpp
                int x = 0;
                String xString;
                RuntimeParameters::TryGetValue(L"x", x);
                RuntimeParameters::TryGetValue(L"x", xString);
```

有关详细信息，请访问[TAEF。运行时参数](runtime-parameters.md)帮助页。

### <a name="span-idparallelspanspan-idparallelspanparallel"></a><span id="parallel"></span><span id="PARALLEL"></span>/parallel

在多个处理器上并行执行测试。 测试必须参加并行执行到由标记为 Parallel 元数据。

**te.exe test1.dll /parallel**

有关详细信息，请访问[并行](parallel.md)帮助页。

### <a name="span-idpersistpictresultsspanspan-idpersistpictresultsspanspan-idpersistpictresultsspanpersistpictresults"></a><span id="persistPictResults"></span><span id="persistpictresults"></span><span id="PERSISTPICTRESULTS"></span>/persistPictResults

缓存通过 PICT.exe 生成使用为测试结果[PICT DataSource](pict-data-source.md)中当前的执行。 后续的测试执行将尝试使用缓存的结果与针对相同的模型和种子文件运行 PICT.exe 相对。

### <a name="span-idpictspanspan-idpictspanpictltoptionnamegtltoptionvaluegt"></a><span id="pict"></span><span id="PICT"></span>/pict:&lt;OptionName&gt;=&lt;OptionValue&gt;

提供了选项，用于控制 PICT.exe 时调用它的测试使用[PICT DataSource](pict-data-source.md)。 当前设置以下选项之一时，会重写代码中的所有关联元数据。 你可使用以下选项：

<span id="_Pict_Order_3"></span><span id="_pict_order_3"></span><span id="_PICT_ORDER_3"></span>/Pict:Order=3  
通过将值传递通过 PICT.exe /o 命令选项设置的组合的顺序。

<span id="_Pict_ValueSeparator__"></span><span id="_pict_valueseparator__"></span><span id="_PICT_VALUESEPARATOR__"></span>/Pict:ValueSeparator=;  
通过将值传递通过 PICT.exe /d 命令选项设置值分隔符。

<span id="_Pict_AliasSeparator__"></span><span id="_pict_aliasseparator__"></span><span id="_PICT_ALIASSEPARATOR__"></span>/Pict:AliasSeparator=+  
通过将值传递通过 PICT.exe / a 命令选项设置别名分隔符。

<span id="_Pict_NegativeValuePrefix__"></span><span id="_pict_negativevalueprefix__"></span><span id="_PICT_NEGATIVEVALUEPREFIX__"></span>/Pict:NegativeValuePrefix=!  
通过将值传递通过 PICT.exe /n 命令选项中设置的负值前缀。

<span id="_pict_seedingfile_test.seed"></span><span id="_PICT_SEEDINGFILE_TEST.SEED"></span>/Pict:SeedingFile=test.seed  
通过将值传递通过 PICT.exe /e 命令选项设置种子设定的文件的路径。

<span id="_Pict_Random_true"></span><span id="_pict_random_true"></span><span id="_PICT_RANDOM_TRUE"></span>/Pict:Random=true  
打开或关闭 PICT 结果中的随机性，并使日志已使用的随机种子 PICT 数据源。

<span id="_Pict_RandomSeed_33"></span><span id="_pict_randomseed_33"></span><span id="_PICT_RANDOMSEED_33"></span>/Pict:RandomSeed=33  
通过将值传递通过 PICT.exe /r 命令选项设置随机种子。 将此项设置将开启 Pict： 随机除非 Pict： 随机显式设置为 false。

<span id="_Pict_CaseSensitive_true"></span><span id="_pict_casesensitive_true"></span><span id="_PICT_CASESENSITIVE_TRUE"></span>/Pict:CaseSensitive=true  
如果设置为 true，将在通过将 /c 命令选项传递到 PICT.exe 是否区分大小写。

<span id="_Pict_Timeout_00_01_30"></span><span id="_pict_timeout_00_01_30"></span><span id="_PICT_TIMEOUT_00_01_30"></span>/Pict:Timeout=00:01:30  
设置等待 PICT.exe 终止其进程之前完成的时间。 值的格式\[天。\]小时\[： 分钟\[： 第二个\[。秒的小数部分\]\]\]。

### <a name="span-idrunasspanspan-idrunasspanrunasltrunastypegt"></a><span id="runas"></span><span id="RUNAS"></span>/runas:&lt;RunAsType&gt;

在指定的环境中执行测试。 请参阅[RunAs](runas.md)文档，以详细使用情况信息。

<span id="te.exe__.dll__runas_System"></span><span id="te.exe__.dll__runas_system"></span><span id="TE.EXE__.DLL__RUNAS_SYSTEM"></span>te.exe \*.dll /runas:System  
**解释：** 作为系统运行所有测试。

<span id="te.exe__.dll__runas_Elevated"></span><span id="te.exe__.dll__runas_elevated"></span><span id="TE.EXE__.DLL__RUNAS_ELEVATED"></span>te.exe \*.dll /runas:Elevated  
**解释：** 作为权限提升的用户运行所有测试。

<span id="te.exe__.dll__runas_Restricted"></span><span id="te.exe__.dll__runas_restricted"></span><span id="TE.EXE__.DLL__RUNAS_RESTRICTED"></span>te.exe \*.dll /runas:Restricted  
**解释：** 以非提升用户身份运行所有测试。

<span id="te.exe__.dll__runas_LowIL"></span><span id="te.exe__.dll__runas_lowil"></span><span id="TE.EXE__.DLL__RUNAS_LOWIL"></span>te.exe \*.dll /runas:LowIL  
**解释：** 在低完整性进程中运行所有测试。

### <a name="span-idrunignoredtestsspanspan-idrunignoredtestsspanspan-idrunignoredtestsspanrunignoredtests"></a><span id="runIgnoredTests"></span><span id="runignoredtests"></span><span id="RUNIGNOREDTESTS"></span>/runIgnoredTests

执行或列出 (如果结合[/list](#list)或[/listProperties](#listproperties)) 所有测试，包括测试类和测试方法使用"忽略"元数据设置为"true"。 由默认测试类和测试执行期间，可以在列表时跳过"忽略"元数据设置为"true"的方法。

### <a name="span-idrunonspanspan-idrunonspanrunonltmachinenamegt"></a><span id="runon"></span><span id="RUNON"></span>/runon:&lt;MachineName&gt;

指定的计算机上远程执行测试。 TAEF 进行身份验证、 授权和部署的必要二进制文件执行的测试，并返回到原始控制台日志的所有信息。 请参阅[跨机器测试执行](cross-machine-execution.md)文档，以详细使用情况信息。

<span id="te.exe__.dll__runon_TestMachine1"></span><span id="te.exe__.dll__runon_testmachine1"></span><span id="TE.EXE__.DLL__RUNON_TESTMACHINE1"></span>te.exe \*.dll /runon:TestMachine1  
**解释：**"TestMachine1"上远程运行所有测试。

### <a name="span-idselectspanspan-idselectspanselectltquerygt"></a><span id="select"></span><span id="SELECT"></span>/select:&lt;query&gt;

选择从每个测试时要使用的选择条件测试二进制文件。 选择条件组成一个或多个以下：

@\[属性名称\] = \[值作为字符串\]
@\[属性名称\] &gt; = \[值作为 float 或 integer\] 
@\[属性名称\] &gt; \[为 float 或 integer 值\]
@\[属性名称\] &lt;= \[值为 float 或 integer\]
@\[属性名称\] &lt; \[为 float 或 integer 值\]
-   *以字符串形式的属性值必须是单引号内。*
-   *你可以指定使用复合选择条件"和"，"和"not"（不区分大小写）。*
-   *属性的字符串值支持通过通配符字符"\*"和"？"字符。*
-   *对于 float 和 integer 值，"\*"字符也可以使用存在，但不能用于部分匹配。* 例如： **/选择:"@Priority=\*"** 有效，但 **/选择:"@Priority= 4\*"** 不是。

<span id="te.exe_test1.dll__select____Name___TestToLower__or__Owner__C2___and_not__Priority___3__"></span><span id="te.exe_test1.dll__select____name___testtolower__or__owner__c2___and_not__priority___3__"></span><span id="TE.EXE_TEST1.DLL__SELECT____NAME___TESTTOLOWER__OR__OWNER__C2___AND_NOT__PRIORITY___3__"></span>te.exe test1.dll /select:"(@Name='\*TestToLower 或@Owner= C2)，而不 (@Priority &lt; 3)"  
**解释：** 在 TestToLower 或其中的 owner 是 C2; 方法名称的结束位置的 test1.dll 中运行所有测试优先级别不小于 3。

<span id="te.exe_test1.dll_test2.dll__select__Priority__"></span><span id="te.exe_test1.dll_test2.dll__select__priority__"></span><span id="TE.EXE_TEST1.DLL_TEST2.DLL__SELECT__PRIORITY__"></span>te.exe test1.dll test2.dll /select:@Priority=\*  
**解释：** 在尚未在其测试元数据指定优先级的 test1.dll 和 test2.dll 中运行所有测试。

<span id="te.exe_test1.dll__select__Name___StringTest__"></span><span id="te.exe_test1.dll__select__name___stringtest__"></span><span id="TE.EXE_TEST1.DLL__SELECT__NAME___STRINGTEST__"></span>te.exe test1.dll /select:@Name='\*StringTest\*  
**解释：** 运行 test1.dll 中的所有测试，其中包含短语 StringTest 命名空间、 类或方法名称中。

### <a name="span-idsessiontimeoutspanspan-idsessiontimeoutspanspan-idsessiontimeoutspansessiontimeoutltvaluegt"></a><span id="sessionTimeout"></span><span id="sessiontimeout"></span><span id="SESSIONTIMEOUT"></span>/sessionTimeout:&lt;value&gt;

设置 Te.exe 整个执行的会话超时值。 如果在超时到期，将适当地中止测试会话，并在进程退出代码将表示出现超时。

**注意：** 必须采用以下格式指定的超时值：

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]] 
```

**注意：** 如果 WTT 下运行，此值可以用于确保即使 TAEF 会话超时时 Wtt 日志文件保持不变。

<span id="te.exe_test1.dll__sessionTimeout_0_0_0.5"></span><span id="te.exe_test1.dll__sessiontimeout_0_0_0.5"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_0_0_0.5"></span>te.exe test1.dll /sessionTimeout:0:0:0.5  
在整个测试会话会在.5 秒后超时。

<span id="te.exe_test1.dll__sessionTimeout_0_0_45"></span><span id="te.exe_test1.dll__sessiontimeout_0_0_45"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_0_0_45"></span>te.exe test1.dll /sessionTimeout:0:0:45  
在整个测试会话将在 45 秒后超时。

<span id="te.exe_test1.dll__sessionTimeout_0_20"></span><span id="te.exe_test1.dll__sessiontimeout_0_20"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_0_20"></span>te.exe test1.dll /sessionTimeout:0:20  
在整个测试会话会在 20 分钟后超时。

<span id="te.exe_test1.dll__sessionTimeout_5"></span><span id="te.exe_test1.dll__sessiontimeout_5"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_5"></span>te.exe test1.dll /sessionTimeout:5  
在整个测试会话将在 5 个小时后超时。

<span id="te.exe_test1.dll__sessionTimeout_1.2"></span><span id="te.exe_test1.dll__sessiontimeout_1.2"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_1.2"></span>te.exe test1.dll /sessionTimeout:1.2  
在整个测试会话会在 1 天 2 小时后超时。

### <a name="span-idterminateonfirstfailurespanspan-idterminateonfirstfailurespanspan-idterminateonfirstfailurespanterminateonfirstfailure"></a><span id="terminateOnFirstFailure"></span><span id="terminateonfirstfailure"></span><span id="TERMINATEONFIRSTFAILURE"></span>/terminateOnFirstFailure

终止测试运行第一次遇到测试失败。 调用该测试的所有拆解操作，但所有后续的测试被标记为已忽略。 由于的已知问题，测试可能会继续运行时使用测试模式。

**te.exe test1.dll /terminateOnFirstFailure**

### <a name="span-idtestdependenciesspanspan-idtestdependenciesspanspan-idtestdependenciesspantestdependenciesltfilesgt"></a><span id="testDependencies"></span><span id="testdependencies"></span><span id="TESTDEPENDENCIES"></span>/testDependencies:&lt;files&gt;

指定部署时使用的其他测试依赖项[跨机器测试执行](cross-machine-execution.md)。 除非提供的完整路径，则将相对于当前目录，不测试目录中搜索 TAEF。

<span id="te.exe__.dll__runon_TestMachine1__TestDependencies_test_.jpg_file1.doc"></span><span id="te.exe__.dll__runon_testmachine1__testdependencies_test_.jpg_file1.doc"></span><span id="TE.EXE__.DLL__RUNON_TESTMACHINE1__TESTDEPENDENCIES_TEST_.JPG_FILE1.DOC"></span>te.exe \*.dll /runon:TestMachine1 /TestDependencies:test\*.jpg;file1.doc  
**解释：** 在"TestMachine1"，并复制上远程运行所有测试测试\*.jpg 和 file1.doc 转移到远程计算机之前执行任何测试。 每个文件规范可包含通配符字符 (test.txt; 测试\*.dll; 等) 以匹配一个或多个文件。

### <a name="span-idtesttimeoutspanspan-idtesttimeoutspanspan-idtesttimeoutspantesttimeoutltvaluegt"></a><span id="testTimeout"></span><span id="testtimeout"></span><span id="TESTTIMEOUT"></span>/testTimeout:&lt;value&gt;

设置 Te.exe 整个执行的全球化测试超时值。 此值将覆盖任何[测试超时](standard-test-metadata.md)设置给定测试正在执行的元数据。

**注意：** 必须采用以下格式指定的超时值：

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]] 
```

**注意：** 结合使用时，将忽略[/inproc](#inproc)。

<span id="te.exe_test1.dll__testTimeout_0_0_0.5"></span><span id="te.exe_test1.dll__testtimeout_0_0_0.5"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_0_0_0.5"></span>te.exe test1.dll /testTimeout:0:0:0.5  
测试和安装程序/清理的每个方法会在.5 秒后超时。

<span id="te.exe_test1.dll__testTimeout_0_0_45"></span><span id="te.exe_test1.dll__testtimeout_0_0_45"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_0_0_45"></span>te.exe test1.dll /testTimeout:0:0:45  
每个测试和安装程序/清理方法将在 45 秒后超时。

<span id="te.exe_test1.dll__testTimeout_0_20"></span><span id="te.exe_test1.dll__testtimeout_0_20"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_0_20"></span>te.exe test1.dll /testTimeout:0:20  
测试和安装程序/清理的每个方法会在 20 分钟后超时。

<span id="te.exe_test1.dll__testTimeout_5"></span><span id="te.exe_test1.dll__testtimeout_5"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_5"></span>te.exe test1.dll /testTimeout:5  
测试和安装程序/清理的每个方法会在 5 个小时后超时。

<span id="te.exe_test1.dll__testTimeout_1.2"></span><span id="te.exe_test1.dll__testtimeout_1.2"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_1.2"></span>te.exe test1.dll /testTimeout:1.2  
测试和安装程序/清理的每个方法会在 1 天 2 小时后超时。

### <a name="span-idunicodeoutputspanspan-idunicodeoutputspanspan-idunicodeoutputspanunicodeoutputlttruefalsegt"></a><span id="unicodeOutput"></span><span id="unicodeoutput"></span><span id="UNICODEOUTPUT"></span>/unicodeOutput:&lt;true/false&gt;

TE 通过管道输送到一个文本文件，它默认情况下输出 unicode。 一个例外是如果你已请求将添加到现有 ANSII 文件 (通过&gt;&gt;)。

若要重写此行为，可以指定 /unicodeOutput:false。 这将强制 TE 始终输出 ANSII 到该文件。

**te.exe test1.dll /unicodeOutput:false &gt; output.txt**

## <a name="span-idloggersettingsspanspan-idloggersettingsspanspan-idloggersettingsspanlogger-settings"></a><span id="LoggerSettings"></span><span id="loggersettings"></span><span id="LOGGERSETTINGS"></span>记录器设置


### <a name="span-idappendwttloggingspanspan-idappendwttloggingspanspan-idappendwttloggingspanappendwttlogging"></a><span id="appendWttLogging"></span><span id="appendwttlogging"></span><span id="APPENDWTTLOGGING"></span>/appendWttLogging

启用 WTT 日志记录时，将追加到日志文件，而不是将其重写。 必须与结合使用[/enableWttLogging](#enablewttlogging)。

<span id="te.exe_test1.dll__enableWttLogging__appendWttLogging"></span><span id="te.exe_test1.dll__enablewttlogging__appendwttlogging"></span><span id="TE.EXE_TEST1.DLL__ENABLEWTTLOGGING__APPENDWTTLOGGING"></span>te.exe test1.dll /enableWttLogging /appendWttLogging  
将创建或附加到名为日志文件*TE.wtl*测试执行完成后。

### <a name="span-idenablewttloggingspanspan-idenablewttloggingspanspan-idenablewttloggingspanenablewttlogging"></a><span id="enableWttLogging"></span><span id="enablewttlogging"></span><span id="ENABLEWTTLOGGING"></span>/enableWttLogging

启用日志记录; WTTWttlog.dll 必须在你的路径中可用。

<span id="te.exe_test1.dll__enableWttLogging"></span><span id="te.exe_test1.dll__enablewttlogging"></span><span id="TE.EXE_TEST1.DLL__ENABLEWTTLOGGING"></span>te.exe test1.dll /enableWttLogging  
将生成一个名为的日志文件*TE.wtl*测试执行完成后。

### <a name="span-iddefaultappdomainspanspan-iddefaultappdomainspanspan-iddefaultappdomainspandefaultappdomain"></a><span id="defaultAppDomain"></span><span id="defaultappdomain"></span><span id="DEFAULTAPPDOMAIN"></span>/defaultAppDomain

在默认应用程序域中执行托管的测试。

<span id="te.exe_managed.test1.dll__defaultAppDomain"></span><span id="te.exe_managed.test1.dll__defaultappdomain"></span><span id="TE.EXE_MANAGED.TEST1.DLL__DEFAULTAPPDOMAIN"></span>te.exe managed.test1.dll /defaultAppDomain  

### <a name="span-iddisableconsoleloggingspanspan-iddisableconsoleloggingspanspan-iddisableconsoleloggingspandisableconsolelogging"></a><span id="disableConsoleLogging"></span><span id="disableconsolelogging"></span><span id="DISABLECONSOLELOGGING"></span>/disableConsoleLogging

禁用控制台日志输出;必须与结合使用[/enableWttLogging](#enablewttlogging)。

**te.exe test1.dll /disableConsoleLogging /enableWttLogging**

### <a name="span-idlogfilespanspan-idlogfilespanspan-idlogfilespanlogfileltnamegt"></a><span id="logFile"></span><span id="logfile"></span><span id="LOGFILE"></span>/logFile:&lt;name&gt;

指定要作为 wtt 日志文件，则使用的名称必须与结合使用[/enableWttLogging](#enablewttlogging)。

<span id="te.exe_test1.dll__logFile_myCustomLogFile.xml__enableWttLogging"></span><span id="te.exe_test1.dll__logfile_mycustomlogfile.xml__enablewttlogging"></span><span id="TE.EXE_TEST1.DLL__LOGFILE_MYCUSTOMLOGFILE.XML__ENABLEWTTLOGGING"></span>te.exe test1.dll /logFile:myCustomLogFile.xml /enableWttLogging  
将生成一个名为的日志文件*myCustomeLogFile.xml*测试执行完成后。

### <a name="span-idlogoutputspanspan-idlogoutputspanspan-idlogoutputspanlogoutputltmodegt"></a><span id="logOutput"></span><span id="logoutput"></span><span id="LOGOUTPUT"></span>/logOutput:&lt;mode&gt;

设置记录器的输出级别。 有效值包括：

-   *高*:启用某些其他控制台输出，例如打印每个跟踪旁边的时间戳。
-   *低*:发出唯一 （开始、 结束组等） 的核心事件和错误。 日志文件包含较低优先级的详细信息前面为故障提供上下文的任何错误。
-   *LowWithConsoleBuffering*:与相同*低*，但包括失败的上下文中的日志文件和控制台输出。
-   *最低*:与相同*低*，但控制台输出包括仅错误、 测试失败和执行的摘要。

### <a name="span-idversionspanspan-idversionspanversion"></a><span id="version"></span><span id="VERSION"></span>/version

输出详细的版本信息。

### <a name="span-idwttdevicestringspanspan-idwttdevicestringspanspan-idwttdevicestringspanwttdevicestringltvaluegt"></a><span id="wttDeviceString"></span><span id="wttdevicestring"></span><span id="WTTDEVICESTRING"></span>/wttDeviceString:&lt;value&gt;

完全重写时初始化 WttLogger 使用 WexLogger WttDeviceString。

**te.exe test1.dll /wttDeviceString:$Console**

### <a name="span-idwttdevicestringsuffixspanspan-idwttdevicestringsuffixspanspan-idwttdevicestringsuffixspanwttdevicestringsuffixltvaluegt"></a><span id="wttDeviceStringSuffix"></span><span id="wttdevicestringsuffix"></span><span id="WTTDEVICESTRINGSUFFIX"></span>/wttDeviceStringSuffix:&lt;value&gt;

为默认值时初始化 WttLogger 使用 WexLogger WttDeviceString 追加指定的值。 如果忽略[wttDeviceString](#wttdevicestringsuffix)还指定了。

**te.exe test1.dll /wttDeviceStringSuffix:$Console**

## <a name="span-iddebugsettingsspanspan-iddebugsettingsspanspan-iddebugsettingsspandebug-settings"></a><span id="DebugSettings"></span><span id="debugsettings"></span><span id="DEBUGSETTINGS"></span>调试设置


### <a name="span-idbreakoncreatespanspan-idbreakoncreatespanspan-idbreakoncreatespanbreakoncreate"></a><span id="breakOnCreate"></span><span id="breakoncreate"></span><span id="BREAKONCREATE"></span>/breakOnCreate

中断到调试器之前实例化每个测试类。

**te.exe test1.dll /breakOnCreate**

### <a name="span-idbreakonerrorspanspan-idbreakonerrorspanspan-idbreakonerrorspanbreakonerror"></a><span id="breakOnError"></span><span id="breakonerror"></span><span id="BREAKONERROR"></span>/breakOnError

如果记录错误或测试失败，则会中断到调试器。

**te.exe test1.dll /breakOnError**

### <a name="span-idbreakoninvokespanspan-idbreakoninvokespanspan-idbreakoninvokespanbreakoninvoke"></a><span id="breakOnInvoke"></span><span id="breakoninvoke"></span><span id="BREAKONINVOKE"></span>/breakOnInvoke

中断到调试器之前调用每个测试方法。

**te.exe test1.dll /breakOnInvoke**

### <a name="span-iddisabletimeoutsspanspan-iddisabletimeoutsspanspan-iddisabletimeoutsspandisabletimeouts"></a><span id="disableTimeouts"></span><span id="disabletimeouts"></span><span id="DISABLETIMEOUTS"></span>/disableTimeouts

在执行过程中禁用所有的超时值。 这在调试时，可避免超时 TAEF 等待正在调试的程序部分时很有用。

**te.exe test1.dll /disableTimeouts**

### <a name="span-idminidumponerrorspanspan-idminidumponerrorspanspan-idminidumponerrorspanminidumponerror"></a><span id="miniDumpOnError"></span><span id="minidumponerror"></span><span id="MINIDUMPONERROR"></span>/miniDumpOnError

采用，并在出现测试错误或失败时记录微型转储。

**te.exe test1.dll /miniDumpOnError**

### <a name="span-idminidumponcrashspanspan-idminidumponcrashspanspan-idminidumponcrashspanminidumponcrash"></a><span id="miniDumpOnCrash"></span><span id="minidumponcrash"></span><span id="MINIDUMPONCRASH"></span>/miniDumpOnCrash

采用和日志小型转储，如果测试故障发生。

**te.exe test1.dll /miniDumpOnCrash**

### <a name="span-idrebootstatefilespanspan-idrebootstatefilespanspan-idrebootstatefilespanrebootstatefile"></a><span id="rebootStateFile"></span><span id="rebootstatefile"></span><span id="REBOOTSTATEFILE"></span>/rebootStateFile

显式允许执行[重新启动](reboot.md)测试。

**te.exe test1.dll /rebootStateFile:myFile.xml**

### <a name="span-idreportloadingissuespanspan-idreportloadingissuespanspan-idreportloadingissuespanreportloadingissue"></a><span id="reportLoadingIssue"></span><span id="reportloadingissue"></span><span id="REPORTLOADINGISSUE"></span>/reportLoadingIssue

TAEF 无法加载测试 dll 时将显示一个对话框，错误说明。 必须仅用于本机单元测试 dll 加载问题的调查。

**te.exe test1.dll /reportLoadingIssue**

### <a name="span-idscreencaptureonerrorspanspan-idscreencaptureonerrorspanspan-idscreencaptureonerrorspanscreencaptureonerror"></a><span id="screenCaptureOnError"></span><span id="screencaptureonerror"></span><span id="SCREENCAPTUREONERROR"></span>/screenCaptureOnError

采用，并在出现测试错误或失败时记录屏幕捕获。

**te.exe test1.dll /screenCaptureOnError**

### <a name="span-idstackframecountspanspan-idstackframecountspanspan-idstackframecountspanstackframecountltvaluegt"></a><span id="stackFrameCount"></span><span id="stackframecount"></span><span id="STACKFRAMECOUNT"></span>/stackFrameCount:&lt;value&gt;

指定要显示获取调用堆栈时的堆栈帧数。 默认值为 50。

**te.exe test1.dll /stackFrameCount:100**

### <a name="span-idstacktraceonerrorspanspan-idstacktraceonerrorspanspan-idstacktraceonerrorspanstacktraceonerror"></a><span id="stackTraceOnError"></span><span id="stacktraceonerror"></span><span id="STACKTRACEONERROR"></span>/stackTraceOnError

采用，并在出现测试错误或失败时记录的堆栈跟踪。

**te.exe test1.dll /stackTraceOnError**

## <a name="span-idtestmodesspanspan-idtestmodesspanspan-idtestmodesspantest-modes"></a><span id="TestModes"></span><span id="testmodes"></span><span id="TESTMODES"></span>测试模式


### <a name="span-idlooptestmodespanspan-idlooptestmodespanspan-idlooptestmodespantestmodeloop"></a><span id="loopTestMode"></span><span id="looptestmode"></span><span id="LOOPTESTMODE"></span>/testmode:Loop

允许控制执行使用两个变量*循环*并*LoopTest*。

-   *循环*:执行控件的整个运行的次数。 默认为 1。
-   *LoopTest*:控制在执行各个测试的次数。 默认值 10。

<span id="te.exe_test1.dll__testmode_Loop"></span><span id="te.exe_test1.dll__testmode_loop"></span><span id="TE.EXE_TEST1.DLL__TESTMODE_LOOP"></span>te.exe test1.dll /testmode:Loop  
**解释：** 执行每个测试中 test1.dll 10 次 (默认值为*LoopTest*)。 整个执行运行一次 (默认值为*循环*)。

<span id="te.exe_test1.dll_test2.dll__testmode_Loop__Loop_3__LoopTest_1"></span><span id="te.exe_test1.dll_test2.dll__testmode_loop__loop_3__looptest_1"></span><span id="TE.EXE_TEST1.DLL_TEST2.DLL__TESTMODE_LOOP__LOOP_3__LOOPTEST_1"></span>te.exe test1.dll test2.dll /testmode:Loop /Loop:3 /LoopTest:1  
**解释：** 每个测试运行 test1.dll 和 test2.dll 中一次 (由*LoopTest*)。 （test1.dll 和 test2.dll 中的所有组合测试） 的整个执行运行 3 次的由*循环*。

### <a name="span-idstressspanspan-idstressspantestmodestress"></a><span id="stress"></span><span id="STRESS"></span>/testmode:Stress

在压力测试模式下，TAEF 测试无限期运行，直到输入 Ctrl + C，或直到 WM\_到 TAEF 的隐藏的窗口发送关闭消息。 必须与结合使用运行 /testmode:stress [/inproc](#inproc)。

**te.exe test1.dll /testmode:Stress /inproc**

有关详细的信息和在此模式下，支持其他参数，请参阅文档[此处](test-modes.md)。










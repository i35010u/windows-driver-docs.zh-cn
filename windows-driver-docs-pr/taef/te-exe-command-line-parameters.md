---
title: Te.exe 命令选项
description: Te.exe 命令选项
ms.assetid: E9A9292D-FA30-410d-9322-BD0F321314F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 502964d420b44ff3a1e89960930ef4d565c0e53b
ms.sourcegitcommit: 69261fa09a48b70a681bec0b4cf7afa8b84c73b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68415095"
---
# <a name="teexe-command-options"></a>Te.exe 命令选项

## <a name="usage"></a>用法

**:::no-loc text="te.exe":::** \<[:::no-loc text="test\_binaries":::](#test_binaries)> \[[:::no-loc text="/appendWttLogging":::](#appendwttlogging)\] \[[:::no-loc text="/breakOnCreate":::](#breakoncreate)\] \[[:::no-loc text="/breakOnError":::](#breakonerror)\] \[[:::no-loc text="/breakOnInvoke":::](#breakoninvoke)\] \[[:::no-loc text="/coloredConsoleOutput":::](#coloredconsoleoutputtruefalse) \] \[ [:::no-loc text="/console:flushWrites":::](#consoleflushwrites) \] \[ [ :::no-loc text="/console:position=\[x,y | current"::: \] ](#consolepositionxy--current-) \[ [ :::no-loc text="/console:size=&lt;x,y&gt;"::: \] ](#consolesize-xy--current-) \[ [ :::no-loc text="/console:topmost":::\]](#consoletopmost) [\[:::no-loc text="/defaultAppDomain":::\]](#defaultappdomain) \[[:::no-loc text="/disableConsoleLogging":::](#disableconsolelogging)\] \[[:::no-loc text="/disableTimeouts":::](#disabletimeouts)\] \[[:::no-loc text="/dpiaware":::](#dpiaware) \] \[[:::no-loc text="/enableWttLogging":::](#enablewttlogging) \] \[ [:::no-loc text="/inproc":::](#inproc) \] \[ [:::no-loc text="/isolationLevel":::](#isolationlevellevel) \] \[ [:::no-loc text="/labMode":::](#labmode) \] \[[:::no-loc text="/list":::](#list)\] \[[:::no-loc text="/listProperties":::](#listproperties)\] \[[:::no-loc text="/logFile:&lt;name&gt;":::](#logfilename)\] \[[:::no-loc text="/logOutput:&lt;mode&gt;":::](#logoutputmode)\] \[[:::no-loc text="/miniDumpOnCrash":::](#minidumponcrash)\] \[[:::no-loc text="/miniDumpOnError":::](#minidumponerror)\] \[[:::no-loc text="/name:&lt;testname&gt;":::](#nametestname)\] \[[:::no-loc text="/outputFolder:&lt;folderName&gt;":::](#outputfolderfoldername)\] \[[:::no-loc text="/p:&lt;ParamName&gt;=&lt;ParamValue&gt;":::](#pparamnameparamvalue) \] \[ [:::no-loc text="/parallel":::](#parallel) \] \[ [:::no-loc text="/persistPictResults":::](#persistpictresults) \] \[ [:::no-loc text="/pict:&lt;OptionName&gt;=&lt;OptionValue&gt;":::](#pictoptionnameoptionvalue) \] [ \[:::no-loc text="/rebootStateFile":::\]](#rebootstatefile) \[[:::no-loc text="/reportLoadingIssue":::](#reportloadingissue)\] \[[:::no-loc text="/runas:&lt;RunAsType&gt;":::](#runasrunastype)\] \[[:::no-loc text="/runIgnoredTests":::](#runignoredtests)\]<s></s>

## <a name="selectionexecution-commands"></a>选择/执行命令

### <a name="test_binaries"></a>test_binaries

指定要执行的一个或多个测试文件 (用空格分隔)。 支持使用通配符。

#### <a name="teexe-test1dll"></a>te test1

**破解**运行 test1 中的所有测试。

#### <a name="teexe-test1dll-test2dll-test3dll"></a>te test1 test2 test3. .dll

**破解**运行 test1、test2 和 test3 中的所有测试。

#### <a name="teexe-dll"></a>\*te .dll

**破解**运行当前目录中所有 dll 中的所有测试。

### <a name="coloredconsoleoutputtruefalse"></a>/coloredConsoleOutput:\<true/false >

指定 TAEF 是否应输出彩色的控制台文本。 默认值为 true。 如果设置为 false, 则 TAEF 将输出默认控制台颜色的所有文本。

`te.exe test1.dll /coloredConsoleOutput:false`

### <a name="consoleoptionnamevalue"></a>/console:\<optionName > =\<value >

提供用于配置 TE 使用控制台的选项。 你可使用以下选项：

#### <a name="consoleflushwrites"></a>/console: flushWrites

导致在写入每个行后刷新控制台输出-在已重定向 TE 的输出时非常有用。

#### <a name="consolepositionxy--current-"></a>/console: position =\[x, y | current\]

设置控制台窗口相对于主监视器角的位置 (以像素为单位)。 使用 "**当前**的值" 指定在从重新启动恢复时, 应存储并使用当前控制台位置。

#### <a name="consolesize-ltxygt--current-"></a>/console: size =\[ &lt;x, y&gt; | 当前\]

设置控制台窗口的大小 (以字符为维度)。 如有必要, 屏幕缓冲区大小将增加以匹配窗口的大小。 使用 "**当前**的值" 指定在从重新启动恢复时, 应存储并使用当前控制台大小。

#### <a name="consoletopmost"></a>/console: 最顶端

在执行期间, 使控制台在桌面 z 顺序中运行 "最顶层"。

### <a name="dpiaware"></a>/dpiaware

在标记为 DPI 感知的进程中执行测试, 请参阅[高 DPI](https://docs.microsoft.com/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)。 还可以通过元数据 ("DpiAware") 设置此设置。

### <a name="inproc"></a>/inproc

执行 TE 进程本身中的所有测试, 而不是在 TE 内执行。ProcessHost。

te test1/inproc

> [!NOTE]
> TE 仅支持在使用 */inproc*设置时一次执行一个测试 dll。

### <a name="isolationlevellevel"></a>/isolationLevel:\<级别 >

指定执行 TAEF 测试时要使用的最低隔离级别。 如果此值与指定为元数据的 IsolationLevel 冲突, 该值将成为具有紧密范围的隔离级别。 有关更多详细信息, 请参阅[测试隔离](test-isolation.md)。

`te.exe test1.dll /isolationLevel:Class`

### <a name="labmode"></a>/labMode

执行测试并删除可能的阻止 UI (例如, 对崩溃测试 Windows 错误报告对话框)。

### <a name="list"></a>/list

列出所有[\_测试二进制文件](#test_binaries)的名称以及其中的类和方法。 如果指定了选择条件, 则仅列出满足条件的那些名称。

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

### <a name="listproperties"></a>/listProperties

列出所有测试\_二进制文件的名称和属性以及其中的类和方法, 以及安装和拆卸函数名称 (如果可用)。 如果指定了选择条件, 则仅列出满足条件的那些名称。

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

### <a name="nametestname"></a>/name:\<testname >

基于测试名称的选择是 "/select:@Name= '&lt;testname&gt;'" 的简单替代方法。 Testname 仍可以包含通配符 ("\*" 和 "？"), 但不能包含在单引号内。&gt; &lt; 如果在命令提示符处同时指定了/select 和/name, 则将优先使用/select 查询, 并忽略/name。

te test1/name:\*TestToLower  

**破解**运行 test1 中的所有测试, 其中方法名称以 "TestToLower" 结尾。 可以使用 "TestToLower" 作为/select:@Name"\*选择条件" 来表示相同的。

te test1/name:\*StringTest\*  

**破解**在命名空间、类或方法名称中包含短语 "StringTest" 的 test1 中运行所有测试。

### <a name="outputfolderfoldername"></a>/outputFolder:\<文件夹名 >

指定放置所有生成的文件的文件夹。 默认值为当前目录。 可以使用环境变量, 例如:

`te.exe test1.dll /outputFolder:%TEMP%\\MyOutput`

### <a name="pparamnameparamvalue"></a>/p:\<ParamName > =\<ParamValue >

用参数 name = ParamName 和参数 value = ParamValue 定义一个运行时参数。 可以通过测试方法或安装/清理方法访问这些参数。

`te.exe test1.dll /p:x=5 /p:myParm=cool`

你可以在测试代码中将 x 作为多种受支持的类型之一。 例如, 你可以看到, 我们将它作为 int 和 WEX:: Common:: String 进行检索:

```cpp
                int x = 0;
                String xString;
                RuntimeParameters::TryGetValue(L"x", x);
                RuntimeParameters::TryGetValue(L"x", xString);
```

有关详细信息, 请访问[TAEF。运行时参数](runtime-parameters.md)帮助页。

### <a name="parallel"></a>/parallel

并行执行多个处理器上的测试。 通过使用 "Parallel" 元数据进行标记, 测试必须选择并行执行。

`te.exe test1.dll /parallel`

有关详细信息, 请访问[并行](parallel.md)帮助页。

### <a name="persistpictresults"></a>/persistPictResults

缓存由 PICT 生成的结果, 以便在当前执行中使用[Pict 数据源](pict-data-source.md)进行测试。 后续的测试执行将尝试使用缓存的结果, 因为对相同的模型和 seed 文件运行 PICT。

### <a name="pictoptionnameoptionvalue"></a>/pict:\<OptionName > =\<OptionValue >

提供使用[Pict 数据源](pict-data-source.md)为测试调用 pict 时用于控制 pict 的选项。 设置其中一个选项当前会覆盖代码中所有关联的元数据。 你可使用以下选项：

/Pict: Order = 3  
通过使用 PICT 的/o 命令选项传递值, 设置组合的顺序。

/Pict: ValueSeparator =;  
通过将值传递给 PICT 的/d 命令选项来设置值分隔符。

/Pict: AliasSeparator = +  
通过使用 PICT 的/a 命令选项传递值来设置别名分隔符。

Pict: NegativeValuePrefix =!  
通过使用 PICT 的/n 命令选项传递值, 设置负值前缀。

/Pict: SeedingFile = test. seed  
通过使用 PICT 的/e 命令选项传递值, 设置播种文件的路径。

/Pict: Random = true  
开启或关闭 PICT 结果中的随机性, 并使 PICT 数据源日志中使用的随机种子。

/Pict: RandomSeed = 33  
通过 PICT 的/r 命令选项传递值, 设置随机种子。 如果设置此选项, 则会启用 Pict: 随机, 除非将 Pict: Random 显式设置为 false。

/Pict: CaseSensitive = true  
如果设置为 true, 则通过将/c 命令选项传递给 PICT 来启用区分大小写。

/Pict: Timeout = 00:01:30  
设置在终止其进程之前等待 PICT 完成的时间。 值的格式\[为 Day。\]小时\[: 分钟\[: 秒\[。FractionalSeconds\]。\]\]

### <a name="runasrunastype"></a>/runas:\<RunAsType >

在指定的环境中执行测试。 有关详细的使用情况信息, 请参阅[RunAs](runas.md)文档。

\*te .dll/runas: System  

**破解**将所有测试作为系统运行。

\*te/runas: 提升  

**破解**以提升的用户身份运行所有测试。

\*te/runas: 受限  

**破解**以非提升用户身份运行所有测试。

\*/runas: LowIL  

**破解**在完整性较低的进程中运行所有测试。

### <a name="runignoredtests"></a>/runIgnoredTests

执行或列出 (如果与[/list](#list)或[/listProperties](#listproperties)一起) 所有测试, 包括将 "Ignore" 元数据设置为 "true" 的测试类和测试方法。 默认情况下, 在执行期间和列出时, 将跳过 "忽略" 设置为 "true" 的测试类和测试方法。

### <a name="runonmachinename"></a>/runon:\<MachineName >

在指定的计算机上远程执行测试。 TAEF 对所需的二进制文件进行身份验证、授权和部署, 以执行测试, 并将所有信息记录回原始控制台。 有关使用情况的详细信息, 请参阅[跨计算机测试执行](cross-machine-execution.md)文档。

\*/runon: TestMachine1

**破解**在 "TestMachine1" 上远程运行所有测试。

### <a name="selectquery"></a>/select:\<查询 >

从每个测试二进制文件选择测试时要使用的选择条件。 选择条件由以下一项或多项组成:

@\[作为 float\]或 integer\[的字符串
@ = \]属性\]名称值的属性名称值\[\[ &gt; = \]\[\] 作为float&lt;或 integer属性名称&gt;的属性名称值\] 
@ \[
@\[\] = \]\[
@作为float\]或 integer 属性名称值的&lt;值\[ \[\]

* *字符串形式的属性值必须用单引号括起来。*
* *您可以使用 "and"、"or" 和 "not" (不区分大小写) 来指定组合选择条件。*
* *属性字符串值通过 "\*" 和 "？" 字符支持通配符。*
* *对于 float 和 integer 值, "\*" 字符也可以用作 "exists", 但不能用于部分匹配。* 例如: **/select: "@Priority\*="** 有效, 但 **/select: "@Priority= 4\*"** 不是。

te test1@Name/select: "(= '\*TestToLower ' or @Owner= ' c2 '), not (@Priority &lt; 3)"

**破解**运行 test1 中的所有测试, 其中方法名称以 "TestToLower" 结尾或所有者为 "C2";, 其中优先级不小于3。

te test1 test2 /select:@Priority=\*

**破解**运行 test1 和 test2 中的所有测试, 其中已在其测试元数据中指定了优先级。

te test1 /select:@Name= '\*StringTest\*'  

**破解**在命名空间、类或方法名称中包含短语 "StringTest" 的 test1 中运行所有测试。

### <a name="sessiontimeoutvalue"></a>/sessionTimeout:\<值 >

为 Te 的整个执行设置会话超时。 如果超时时间已到, 则测试会话将正常中止, 进程退出代码将表示发生了超时。

> [!NOTE]
> 必须按以下格式指定超时值:

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]]
```

> [!NOTE]
> 如果在 WTT 下运行, 则可以使用此值来确保即使 TAEF 会话超时, Wtt 日志文件仍保持不变。

te test1/sessionTimeout: 0: 0: 0。5  

整个测试会话将在5秒后超时。

te test1/sessionTimeout: 0: 0:45  

整个测试会话将在45秒后超时。

te test1/sessionTimeout: 0:20  

整个测试会话将在20分钟后超时。

te test1/sessionTimeout: 5  

整个测试会话将在5小时后超时。

te test1/sessionTimeout: 1。2  

整个测试会话将在1天到2小时后超时。

### <a name="terminateonfirstfailure"></a>/terminateOnFirstFailure

第一次遇到测试失败时终止测试运行。 该测试的所有拆卸操作都将被调用, 但所有后续测试都标记为已忽略。 由于已知问题, 在使用测试模式时, 测试可能会继续运行。

`te.exe test1.dll /terminateOnFirstFailure`

### <a name="testdependenciesfiles"></a>/testDependencies:\<文件 >

指定使用[跨计算机测试执行](cross-machine-execution.md)时要部署的其他测试依赖项。 如果未提供完整路径, TAEF 将搜索相对于当前目录而不是测试目录。

te/runon: TestMachine1/TestDependencies\*:; file1 \*  

**破解**在 "TestMachine1" 上远程运行所有测试, 并在执行\*任何测试之前, 将 "test.txt" 和 "file1" 复制到远程计算机。 每个文件规范都可以包含通配符 (test.txt;\*test.txt; 等等) 以匹配一个或多个文件。

### <a name="testtimeoutvalue"></a>/testTimeout:\<值 >

为 Te 的整个执行设置全局测试超时。 此值将覆盖可能已为正在执行的给定测试设置的任何[测试](standard-test-metadata.md)超时元数据。

> [!NOTE]
> 必须按以下格式指定超时值:

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]]
```

> [!NOTE]
> 与[/inproc](#inproc)一起使用时, 将被忽略。

te test1/testTimeout: 0: 0: 0。5  

每个测试和安装/清理方法将在5秒后超时。

te test1/testTimeout: 0: 0:45  

每个测试和安装/清理方法将在45秒后超时。

te test1/testTimeout: 0:20  

每个测试和安装/清理方法将在20分钟后超时。

te test1/testTimeout: 5  

每个测试和安装/清理方法将在5小时后超时。

te test1/testTimeout: 1。2  

每个测试和安装/清理方法将在1天和2小时后超时。

### <a name="unicodeoutputtruefalse"></a>/unicodeOutput:\<true/false >

当 TE 传输到文本文件时, 它会默认输出 unicode。 这种情况的一个例外是, 如果你已请求追加到现有的 ANSII 文件 (通过&gt;"&gt;")。

若要重写此行为, 可以指定/unicodeOutput: false。 这将强制 TE 始终将 ANSII 输出到该文件。

`te.exe test1.dll /unicodeOutput:false > output.txt`

## <a name="logger-settings"></a>记录器设置

### <a name="appendwttlogging"></a>/appendWttLogging

启用 WTT 日志记录时, 会将追加到日志文件, 而不是覆盖它。 必须与[/enableWttLogging](#enablewttlogging)结合使用。

te test1/enableWttLogging/appendWttLogging  

完成测试执行时, 将创建或追加到名为*wtl*的日志文件。

### <a name="enablewttlogging"></a>/enableWttLogging

启用 WTT 日志记录;Wttlog 必须在你的路径中可用。

te test1/enableWttLogging

完成测试执行时, 将生成一个名为*wtl*的日志文件。

### <a name="defaultappdomain"></a>/defaultAppDomain

在默认应用程序域中执行托管测试。

te 管理的/defaultAppDomain  

### <a name="disableconsolelogging"></a>/disableConsoleLogging

禁用控制台日志输出;必须与[/enableWttLogging](#enablewttlogging)结合使用。

`te.exe test1.dll /disableConsoleLogging /enableWttLogging`

### <a name="logfilename"></a>/logFile:\<name >

指定要用作 wtt 日志文件的名称;必须与[/enableWttLogging](#enablewttlogging)结合使用。

te test1/logFile: myCustomLogFile/enableWttLogging  

完成测试执行时, 将生成一个名为*myCustomeLogFile*的日志文件。

### <a name="logoutputmode"></a>/logOutput:\<mode >

设置记录器的输出级别。 有效值包括：

* *高*:启用其他一些控制台输出, 例如打印每个跟踪旁边的时间戳。
* *低*:仅发出核心事件 (开始、结束组等) 和错误。 该日志文件包含之前的优先级较低的详细信息, 以提供失败的上下文。
* *LowWithConsoleBuffering*:与*Low*相同, 但包含日志文件和控制台输出中的失败的上下文。
* *最低*:与*Low*相同, 但控制台输出只包含错误、测试失败和执行摘要。

### <a name="version"></a>/version

输出详细的版本信息。

### <a name="wttdevicestringvalue"></a>/wttDeviceString:\<值 >

初始化 WttLogger 时, 完全重写 WexLogger 使用的 WttDeviceString。

`te.exe test1.dll /wttDeviceString:$Console`

### <a name="wttdevicestringsuffixvalue"></a>/wttDeviceStringSuffix:\<值 >

当初始化 WttLogger 时, 将指定的值追加到 WexLogger 使用的默认 WttDeviceString。 如果同时指定了[wttDeviceString](#wttdevicestringvalue) , 则忽略。

`te.exe test1.dll /wttDeviceStringSuffix:$Console`

## <a name="debug-settings"></a>调试设置

### <a name="breakoncreate"></a>/breakOnCreate

在实例化每个测试类之前中断到调试器。

`te.exe test1.dll /breakOnCreate`

### <a name="breakonerror"></a>/breakOnError

如果记录错误或测试错误, 则中断调试器。

`te.exe test1.dll /breakOnError`

### <a name="breakoninvoke"></a>/breakOnInvoke

在调用每个测试方法之前中断调试器。

`te.exe test1.dll /breakOnInvoke`

### <a name="disabletimeouts"></a>/disableTimeouts

在执行过程中禁用所有超时。 当 TAEF 等待正在调试的程序的部分时, 这会在调试时非常有用。

`te.exe test1.dll /disableTimeouts`

### <a name="minidumponerror"></a>/miniDumpOnError

如果发生测试错误或失败, 则使用并记录小型转储。

`te.exe test1.dll /miniDumpOnError`

### <a name="minidumponcrash"></a>/miniDumpOnCrash

如果发生测试崩溃, 则使用并记录小型转储。

`te.exe test1.dll /miniDumpOnCrash`

### <a name="rebootstatefile"></a>/rebootStateFile

显式启用[重新启动](reboot.md)测试的执行。

`te.exe test1.dll /rebootStateFile:myFile.xml`

### <a name="reportloadingissue"></a>/reportLoadingIssue

当 TAEF 无法加载测试 dll 时, 将显示 "错误说明" 对话框。 必须仅用于调查本机测试 dll 加载问题。

`te.exe test1.dll /reportLoadingIssue`

### <a name="screencaptureonerror"></a>/screenCaptureOnError

如果发生测试错误或失败, 则将使用并记录屏幕捕获。

`te.exe test1.dll /screenCaptureOnError`

### <a name="stackframecountvalue"></a>/stackFrameCount:\<值 >

指定在获取调用堆栈时要显示的堆栈帧的数目。 默认值为50。

`te.exe test1.dll /stackFrameCount:100`

### <a name="stacktraceonerror"></a>/stackTraceOnError

如果发生测试错误或失败, 则使用并记录堆栈跟踪。

`te.exe test1.dll /stackTraceOnError`

## <a name="test-modes"></a>测试模式

### <a name="testmodeloop"></a>/testmode: 循环

允许使用两个变量*循环*和*LoopTest*控制执行。

* *循环*:控制执行整个运行的次数。 默认值为1。
* *LoopTest*:控制执行单个测试的次数。 默认值为10。

te test1/testmode: Loop  

**破解**运行 test1 10 次中的每个测试 ( *LoopTest*的默认值)。 整个执行只运行一次 (*循环*的默认值)。

te test1 test2/testmode: 循环/Loop: 3/LoopTest: 1  

**破解**运行 test1 和 test2 中的每个测试一次 (由*LoopTest*决定)。 整个执行 (test1 和 test2 中的所有组合测试) 运行3次, 这是由*循环*确定的。

### <a name="testmodestress"></a>/testmode: 压力

在 "压力" 测试模式下, TAEF 会无限期地运行测试, 直到输入 Ctrl + C 或将\_WM CLOSE 消息发送到 TAEF 的隐藏窗口。 /testmode: 压力必须与[/inproc](#inproc)一起运行。

`te.exe test1.dll /testmode:Stress /inproc`

有关此模式下支持的详细信息和其他参数, 请参阅[测试模式](test-modes.md)。

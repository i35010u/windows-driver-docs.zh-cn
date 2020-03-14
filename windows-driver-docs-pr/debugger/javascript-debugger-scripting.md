---
title: JavaScript 调试器脚本
description: 本主题介绍如何使用 JavaScript 创建脚本，这些脚本可理解调试器对象和扩展和自定义调试器的功能。
ms.assetid: 3442E2C4-4054-4698-B7FB-8FE19D26C171
ms.date: 04/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: b01aed239dabef52d3fcd3a37c1feb56b1f5920b
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242784"
---
# <a name="javascript-debugger-scripting"></a>JavaScript 调试器脚本


本主题介绍如何使用 JavaScript 创建脚本，这些脚本可理解调试器对象和扩展和自定义调试器的功能。

## <a name="span-idoverview_of_javascript_debugger_scripting_spanspan-idoverview_of_javascript_debugger_scripting_spanspan-idoverview_of_javascript_debugger_scripting_spanoverview-of-javascript-debugger-scripting"></a><span id="Overview_of_JavaScript_Debugger_Scripting_"></span><span id="overview_of_javascript_debugger_scripting_"></span><span id="OVERVIEW_OF_JAVASCRIPT_DEBUGGER_SCRIPTING_"></span>JavaScript 调试器脚本概述


脚本提供程序将脚本语言桥接到调试器的内部对象模型中。 JavaScript 调试器脚本提供程序允许将 JavaScript 用于调试器。

当通过 scriptload 命令加载 JavaScript 时，将执行该脚本的根代码，脚本中存在的名称将桥接到调试器的根命名空间中（dx 调试器），脚本会一直驻留在内存中，直到它被卸载，释放对其对象的所有引用。 此脚本可以为调试器的表达式计算器提供新函数，修改调试器的对象模型，或以 NatVis 可视化工具的相同方式充当可视化工具。

本主题介绍了一些可以通过 JavaScript 调试器脚本执行的操作。

这两个主题提供了有关在调试器中使用 JavaScript 的其他信息。

[JavaScript 调试器示例脚本](javascript-debugger-example-scripts.md)

[JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)


## <a name="javascript-scripting-video"></a>JavaScript 脚本撰写视频

[碎片整理工具 #170](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-170-Debugger-JavaScript-Scripting) -脚本和帐单演示了调试程序中的 JavaScript 扩展性和脚本功能。


## <a name="span-idproviderspanspan-idproviderspanspan-idproviderspanthe-debugger-javascript-provider"></a><span id="Provider"></span><span id="provider"></span><span id="PROVIDER"></span>调试器 JavaScript 提供程序

调试器附带的 JavaScript 提供程序充分利用了最新的 ECMAScript6 对象和类增强功能。 有关详细信息，请参阅[ECMAScript 6-新增功能：概述 & 比较](https://es6-features.org/)。

**JsProvider**

JsProvider 是为支持 JavaScript 调试器脚本而加载的 JavaScript 提供程序。

**要求**

JavaScript 调试器脚本设计为适用于所有受支持的 Windows 版本。

## <a name="span-idloading_the_javascript_scripting_providerspanspan-idloading_the_javascript_scripting_providerspanspan-idloading_the_javascript_scripting_providerspanloading-the-javascript-scripting-provider"></a><span id="Loading_the_JavaScript_Scripting_Provider"></span><span id="loading_the_javascript_scripting_provider"></span><span id="LOADING_THE_JAVASCRIPT_SCRIPTING_PROVIDER"></span>正在加载 JavaScript 脚本提供程序


使用任何脚本命令之前，需要使用[**加载（加载扩展 DLL）** ](-load---loadby--load-extension-dll-.md)命令加载脚本提供程序。 若要加载 JavaScript 提供程序，请使用以下命令。

```dbgcmd
0:000> .load jsprovider.dll
```

使用 scriptproviders 命令确认已加载 JavaScript 提供程序。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

## <a name="span-idcommandsspanspan-idcommandsspanspan-idcommandsspanjavascript-scripting-meta-commands"></a><span id="Commands"></span><span id="commands"></span><span id="COMMANDS"></span>JavaScript 脚本元命令


以下命令可用于使用 JavaScript 调试器脚本。

-   [ **. scriptproviders （List Script Providers）** ](-scriptproviders--list-script-providers-.md)
-   [ **. scriptload （加载脚本）** ](-scriptload--load-script-.md)
-   [**scriptunload （卸载脚本）** ](-scriptunload--unload-script-.md)
-   [**scriptrun （运行脚本）** ](-scriptrun--run-script-.md)
-   [ **. scriptlist （列出加载的脚本）** ](-scriptlist--list-loaded-scripts-.md)

**要求**

使用任何脚本命令之前，需要使用[**加载（加载扩展 DLL）** ](-load---loadby--load-extension-dll-.md)命令加载脚本提供程序。 若要加载 JavaScript 提供程序，请使用以下命令。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idscriptproviders__list_script_providers_spanspan-idscriptproviders__list_script_providers_spanscriptproviders-list-script-providers"></a><span id=".scriptproviders__list_script_providers_"></span><span id=".SCRIPTPROVIDERS__LIST_SCRIPT_PROVIDERS_"></span>. scriptproviders （List Script Providers）


Scriptproviders 命令将列出调试器当前可以理解的所有脚本语言及其注册的扩展。

在下面的示例中，加载了 JavaScript 和 NatVis 提供程序。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

以 "结尾的任何文件。NatVis "被理解为 NatVis 脚本，以" .js "结尾的任何文件都理解为 JavaScript 脚本。 可以通过 scriptload 命令加载任意一种类型的脚本。

有关详细信息，请参阅[ **Scriptproviders （List Script Providers）** ](-scriptproviders--list-script-providers-.md)

## <a name="span-idscriptload__load_script_spanspan-idscriptload__load_script_spanscriptload-load-script"></a><span id=".scriptload__load_script_"></span><span id=".SCRIPTLOAD__LOAD_SCRIPT_"></span>. scriptload （加载脚本）


Scriptload 命令将加载脚本，并执行脚本和*initializeScript*函数的根代码。 如果脚本的初始加载和执行中有任何错误，则错误将显示在控制台中。 以下命令显示 TestScript 的成功加载。

```dbgcmd
0:000> .scriptload C:\WinDbg\Scripts\TestScript.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\TestScript.js'
```

脚本所执行的任何对象模型操作都将保持不变，直到脚本随后被卸载或再次使用不同内容运行。

有关详细信息，请参阅[ **. Scriptload （加载脚本）** ](-scriptload--load-script-.md)

## <a name="span-idscriptrunspanscriptrun"></a><span id=".SCRIPTRUN"></span>.scriptrun


Scriptrun 命令将加载脚本，执行脚本的根代码、 *initializeScript*和*invokeScript*函数。 如果脚本的初始加载和执行中有任何错误，则错误将显示在控制台中。

```dbgcmd
0:000> .scriptrun C:\WinDbg\Scripts\helloWorld.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\helloWorld.js'
Hello World!  We are in JavaScript!
```

脚本所执行的任何调试器对象模型操作都将保持不变，直到随后卸载脚本或再次使用不同内容运行。

有关详细信息，请参阅 " [**scriptrun （运行脚本）** ](-scriptrun--run-script-.md)"。

## <a name="span-idscriptunload__unload_script_spanspan-idscriptunload__unload_script_spanscriptunload-unload-script"></a><span id=".scriptunload__unload_script_"></span><span id=".SCRIPTUNLOAD__UNLOAD_SCRIPT_"></span>scriptunload （卸载脚本）


Scriptunload 命令卸载已加载的脚本并调用*uninitializeScript*函数。 使用以下命令语法卸载脚本

```dbgcmd
0:000:x86> .scriptunload C:\WinDbg\Scripts\TestScript.js
JavaScript script unloaded from 'C:\WinDbg\Scripts\TestScript.js'
```

有关详细信息，请参阅[**scriptunload （卸载脚本）** ](-scriptunload--unload-script-.md)。

## <a name="span-idscriptlist__list_loaded_scripts_spanspan-idscriptlist__list_loaded_scripts_spanscriptlist-list-loaded-scripts"></a><span id=".scriptlist__list_loaded_scripts_"></span><span id=".SCRIPTLIST__LIST_LOADED_SCRIPTS_"></span>. scriptlist （列出加载的脚本）


Scriptlist 命令将列出已通过 scriptload 或 scriptrun 命令加载的任何脚本。 如果使用 scriptload 成功加载了 TestScript，则 scriptlist 命令会显示加载的脚本的名称。

```dbgcmd
0:000> .scriptlist
Command Loaded Scripts:
    JavaScript script from 'C:\WinDbg\Scripts\TestScript.js'
```

有关详细信息，请参阅[**scriptlist （列出加载的脚本）** ](-scriptlist--list-loaded-scripts-.md)。

## <a name="span-idstartedspanspan-idstartedspanspan-idstartedspanget-started-with-javascript-debugger-scripting"></a><span id="Started"></span><span id="started"></span><span id="STARTED"></span>JavaScript 调试器脚本入门


### <a name="span-idhelloworld_example_scriptspanspan-idhelloworld_example_scriptspanspan-idhelloworld_example_scriptspanhelloworld-example-script"></a><span id="HelloWorld_Example_Script"></span><span id="helloworld_example_script"></span><span id="HELLOWORLD_EXAMPLE_SCRIPT"></span>HelloWorld 示例脚本

本部分介绍如何创建和执行打印 Hello World 的简单 JavaScript 调试器脚本。

```dbgcmd
// WinDbg JavaScript sample
// Prints Hello World
function initializeScript()
{
    host.diagnostics.debugLog("***> Hello World! \n");
}
```

使用文本编辑器（如记事本）创建一个名为*HelloWorld*的文本文件，该文件包含上面所示的 JavaScript 代码。

使用[**load （Load EXTENSION DLL）** ](-load---loadby--load-extension-dll-.md)命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用 scriptload 命令加载和执行脚本。 由于我们使用了函数名称*initializeScript*，因此在加载脚本时将运行该函数中的代码。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\HelloWorld.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\HelloWorld.js'
***> Hello World! 
```

加载脚本后，调试器中会提供其他功能。 使用[**dx （显示 NatVis Expression）** ](dx--display-visualizer-variables-.md)命令显示*调试程序。* 请注意，我们的脚本现已驻留。

```dbgcmd
0:000> dx Debugger.State.Scripts
Debugger.State.Scripts                
    HelloWorld 
```

在下面的示例中，我们将添加并调用一个命名函数。

### <a name="span-idadding_two_values_example_scriptspanspan-idadding_two_values_example_scriptspanspan-idadding_two_values_example_scriptspanadding-two-values-example-script"></a><span id="Adding_Two_Values_Example_Script"></span><span id="adding_two_values_example_script"></span><span id="ADDING_TWO_VALUES_EXAMPLE_SCRIPT"></span>添加两个值示例脚本

本部分介绍如何创建和执行一个简单的 JavaScript 调试器脚本，该脚本添加了输入并添加了两个数字。

这个简单的脚本提供了一个函数 addTwoValues。

```dbgcmd
// WinDbg JavaScript sample
// Adds two functions
function addTwoValues(a, b)
 {
     return a + b;
 }
```

使用文本编辑器（如记事本）创建名为*FirstSampleFunction*的文本文件

使用[**load （Load EXTENSION DLL）** ](-load---loadby--load-extension-dll-.md)命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用 scriptload 命令加载脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\FirstSampleFunction.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\FirstSampleFunction.js'
```

加载脚本后，调试器中会提供其他功能。 使用[**dx （显示 NatVis Expression）** ](dx--display-visualizer-variables-.md)命令显示*调试程序。* 请注意，我们的脚本现已驻留。

```dbgcmd
0:000> dx Debugger.State.Scripts
Debugger.State.Scripts                
    FirstSampleFunction    
```

可以单击*FirstSampleFunction*以查看它提供的功能。

```dbgcmd
0:000> dx -r1 -v Debugger.State.Scripts.FirstSampleFunction.Contents
Debugger.State.Scripts.FirstSampleFunction.Contents                 : [object Object]
    host             : [object Object]
    addTwoValues    
 ... 
```

为了更方便地使用该脚本，请在调试器中分配一个变量，以便使用 dx 命令保存该脚本的内容。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.FirstSampleFunction.Contents
```

使用 dx 表达式计算器调用 addTwoValues 函数。

```dbgcmd
0:000> dx @$myScript.addTwoValues(10, 41),d
@$myScript.addTwoValues(10, 41),d : 51
```

你还可以使用 *@ $scriptContents*内置别名来处理脚本。 *@ $ScriptContents*别名将合并所有。所有加载的脚本的内容。

```dbgcmd
0:001> dx @$scriptContents.addTwoValues(10, 40),d
@$scriptContents.addTwoValues(10, 40),d : 50
```

使用完脚本后，请使用 scriptunload 命令卸载脚本。

```dbgcmd
0:000> .scriptunload c:\WinDbg\Scripts\FirstSampleFunction.js
JavaScript script successfully unloaded from 'c:\WinDbg\Scripts\FirstSampleFunction.js'
```

### <a name="span-idautomatespanspan-idautomatespanspan-idautomatespandebugger-command-automation"></a><span id="Automate"></span><span id="automate"></span><span id="AUTOMATE"></span>调试器命令自动化

本部分介绍如何创建和执行简单的 JavaScript 调试器脚本，以自动发送[**u （Unassemble）** ](u--unassemble-.md)命令。 该示例还演示如何在循环中收集和显示命令输出。

此脚本提供单个函数 RunCommands （）。

```javascript
// WinDbg JavaScript sample
// Shows how to call a debugger command and display results
"use strict";

function RunCommands()
{
var ctl = host.namespace.Debugger.Utility.Control;   
var output = ctl.ExecuteCommand("u");
host.diagnostics.debugLog("***> Displaying command output \n");

for (var line of output)
   {
   host.diagnostics.debugLog("  ", line, "\n");
   }

host.diagnostics.debugLog("***> Exiting RunCommands Function \n");

}
```

使用文本编辑器（如记事本）创建名为*RunCommands*的文本文件

使用[**load （Load EXTENSION DLL）** ](-load---loadby--load-extension-dll-.md)命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用 scriptload 命令加载 RunCommands 脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\RunCommands.js 
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\RunCommands.js'
```

加载脚本后，调试器中会提供其他功能。 使用[**dx （显示 NatVis Expression）** ](dx--display-visualizer-variables-.md)命令显示*RunCommands* ，以了解我们的脚本现在为常驻。

```dbgcmd
0:000>dx -r3 Debugger.State.Scripts.RunCommands
Debugger.State.Scripts.RunCommands                
    Contents         : [object Object]
        host             : [object Object]
            diagnostics      : [object Object]
            namespace       
            currentSession   : Live user mode: <Local>
            currentProcess   : notepad.exe
            currentThread    : ntdll!DbgUiRemoteBreakin (00007ffd`87f2f440) 
            memory           : [object Object]
```

使用 dx 命令调用 RunCommands 脚本中的 RunCommands 函数。

```dbgcmd
0:000> dx Debugger.State.Scripts.RunCommands.Contents.RunCommands()
  ***> Displaying command output
  ntdll!ExpInterlockedPopEntrySListEnd+0x17 [d:\rs1\minkernel\ntos\rtl\amd64\slist.asm @ 196]:
  00007ffd`87f06e67 cc              int     3
  00007ffd`87f06e68 cc              int     3
  00007ffd`87f06e69 0f1f8000000000  nop     dword ptr [rax]
  ntdll!RtlpInterlockedPushEntrySList [d:\rs1\minkernel\ntos\rtl\amd64\slist.asm @ 229]:
  00007ffd`87f06e70 0f0d09          prefetchw [rcx]
  00007ffd`87f06e73 53              push    rbx
  00007ffd`87f06e74 4c8bd1          mov     r10,rcx
  00007ffd`87f06e77 488bca          mov     rcx,rdx
  00007ffd`87f06e7a 4c8bda          mov     r11,rdx
***> Exiting RunCommands Function
```

## <a name="span-idspecial_javascript_debugger_functionsspanspan-idspecial_javascript_debugger_functionsspanspan-idspecial_javascript_debugger_functionsspanspecial-javascript-debugger-functions"></a><span id="Special_JavaScript_Debugger_Functions"></span><span id="special_javascript_debugger_functions"></span><span id="SPECIAL_JAVASCRIPT_DEBUGGER_FUNCTIONS"></span>特殊 JavaScript 调试器函数


脚本提供程序本身调用的 JavaScript 脚本中有几个特殊函数。

### <a name="span-idinitializescriptspanspan-idinitializescriptspanspan-idinitializescriptspaninitializescript"></a><span id="initializeScript"></span><span id="initializescript"></span><span id="INITIALIZESCRIPT"></span>initializeScript

当 JavaScript 脚本加载并执行时，它会经历一系列步骤，然后脚本中的变量、函数和其他对象会影响调试器的对象模型。

-   脚本将加载到内存中并进行分析。
-   执行脚本中的根代码。
-   如果脚本具有一个名为 initializeScript 的方法，则调用该方法。
-   InitializeScript 的返回值用于确定如何自动修改调试器的对象模型。
-   脚本中的名称将桥接到调试器的命名空间。

如前所述，执行脚本的根代码后将立即调用 initializeScript。 其工作是将注册对象的 JavaScript 数组返回给提供程序，指示如何修改调试器的对象模型。

```javascript
function initializeScript()
{
    // Add code here that you want to run every time the script is loaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> initializeScript was called\n");
}
```

### <a name="span-idinvokescriptspanspan-idinvokescriptspanspan-idinvokescriptspaninvokescript"></a><span id="invokeScript"></span><span id="invokescript"></span><span id="INVOKESCRIPT"></span>invokeScript

InvokeScript 方法是主脚本方法，在 scriptload 和 scriptrun 运行时调用。

```javascript
function invokeScript()
{
    // Add code here that you want to run every time the script is executed. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> invokeScript was called\n");
}
```

### <a name="span-iduninitializescriptspanspan-iduninitializescriptspanspan-iduninitializescriptspanuninitializescript"></a><span id="uninitializeScript"></span><span id="uninitializescript"></span><span id="UNINITIALIZESCRIPT"></span>uninitializeScript

UninitializeScript 方法是相对 initializeScript 的行为。 当脚本已取消链接并准备好卸载时，会调用此方法。 它的工作是撤消对对象模型的任何更改，脚本在执行期间强制执行，并/或销毁脚本缓存的任何对象。

如果脚本既不向对象模型发出命令式操作，也不缓存结果，则无需使用 uninitializeScript 方法。 由 initializeScript 的返回值所指示的对象模型的任何更改都会由提供程序自动撤消。 此类更改不需要显式的 uninitializeScript 方法。

```javascript
function uninitializeScript()
{
    // Add code here that you want to run every time the script is unloaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> uninitialize was called\n");
}
```

## <a name="span-idsummary_of_functions_called_by_script_commandsspanspan-idsummary_of_functions_called_by_script_commandsspanspan-idsummary_of_functions_called_by_script_commandsspansummary-of-functions-called-by-script-commands"></a><span id="Summary_of_Functions_Called_by_Script_Commands"></span><span id="summary_of_functions_called_by_script_commands"></span><span id="SUMMARY_OF_FUNCTIONS_CALLED_BY_SCRIPT_COMMANDS"></span>脚本命令调用的函数摘要


下表总结了脚本命令调用的函数

||[.scriptload](-scriptload--load-script-.md)|[scriptrun （运行脚本）](-scriptrun--run-script-.md)|[scriptunload （卸载脚本）](-scriptunload--unload-script-.md)|
|--- |--- |--- |--- |
|root|是|是| | |
|initializeScript|是|是| | |
|invokeScript       | |是| |
|uninitializeScript | ||是|


使用此示例代码可查看在加载、执行和卸载脚本时每个函数的调用时间。

```javascript
// Root of Script
host.diagnostics.debugLog("***>; Code at the very top (root) of the script is always run \n");


function initializeScript()
{
    // Add code here that you want to run every time the script is loaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; initializeScript was called \n");
}

function invokeScript()
{
    // Add code here that you want to run every time the script is executed. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; invokeScript was called \n");
}


function uninitializeScript()
{
    // Add code here that you want to run every time the script is unloaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; uninitialize was called\n");
}


function main()
{
    // main is just another function name in JavaScript
    // main is not called by .scriptload or .scriptrun  
    host.diagnostics.debugLog("***>; main was called \n");
}
```

## <a name="span-idvisualizerspanspan-idvisualizerspanspan-idvisualizerspancreating-a-debugger-visualizer-in-javascript"></a><span id="Visualizer"></span><span id="visualizer"></span><span id="VISUALIZER"></span>在 JavaScript 中创建调试器可视化工具


自定义可视化文件允许您对可视化结构中的数据进行分组和组织，以便更好地反映数据关系和内容。 您可以使用 JavaScript 调试器扩展来编写调试可视化工具，它的操作方式与 NatVis 非常相似。 这是通过创作作为给定数据类型的可视化工具的 JavaScript 原型对象（或 ES6 类）来实现的。 有关 NatVis 和调试器的详细信息，请参阅[**dx （显示 NatVis 表达式）** ](dx--display-visualizer-variables-.md)。

**示例类-Simple1DArray**

假设有一个表示一C++维数组的类的示例。 此类有两个成员： m\_大小，这是数组的总大小，m\_pValues，它是指向内存中等于 m\_大小字段的多个整数的指针。

```cpp
class Simple1DArray
{
private:

    ULONG64 m_size;
    int *m_pValues;
};
```

可以使用 dx 命令查看默认的数据结构呈现。

```dbgcmd
0:000> dx g_array1D
g_array1D                 [Type: Simple1DArray]
    [+0x000] m_size           : 0x5 [Type: unsigned __int64]
    [+0x008] m_pValues        : 0x8be32449e0 : 0 [Type: int *]
```

**JavaScript 可视化工具**

为了使此类型可视化，我们需要创作一个原型（或 ES6）类，该类包含我们希望调试器显示的所有字段和属性。 我们还需要让 initializeScript 方法返回一个对象，该对象通知 JavaScript 提供程序将原型作为给定类型的可视化工具进行链接。

```javascript
function initializeScript()
{
    //
    // Define a visualizer class for the object.
    //
    class myVisualizer
    {
        //
        // Create an ES6 generator function which yields back all the values in the array.
        //
        *[Symbol.iterator]()
        {
            var size = this.m_size;
            var ptr = this.m_pValues;
            for (var i = 0; i < size; ++i)
            {
                yield ptr.dereference();

                //
                // Note that the .add(1) method here is effectively doing pointer arithmetic on
                // the underlying pointer.  It is moving forward by the size of 1 object.
                //
                ptr = ptr.add(1);
            }
        }
    }

    return [new host.typeSignatureRegistration(myVisualizer, "Simple1DArray")];
}
```

将该脚本保存到名为 arrayVisualizer 的文件中。

使用[**load （Load EXTENSION DLL）** ](-load---loadby--load-extension-dll-.md)命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

使用 scriptload 加载数组可视化工具脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\arrayVisualizer.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\arrayVisualizer.js'
```

现在，使用 dx 命令时，脚本可视化工具将显示数组内容的行。

```dbgcmd
0:000> dx g_array1D
g_array1D                 : [object Object] [Type: Simple1DArray]
    [<Raw View>]     [Type: Simple1DArray]
    [0x0]            : 0x0
    [0x1]            : 0x1
    [0x2]            : 0x2
    [0x3]            : 0x3
    [0x4]            : 0x4
```

此外，此 JavaScript 可视化提供了 LINQ 功能，如 Select。

```dbgcmd
0:000> dx g_array1D.Select(n => n * 3),d
g_array1D.Select(n => n * 3),d                
    [0]              : 0
    [1]              : 3
    [2]              : 6
    [3]              : 9
    [4]              : 12
```

**影响可视化效果的内容**

一个原型或类，它通过从 initializeScript 中返回的 typeSignatureRegistration 对象，将 JavaScript 中的所有属性和方法添加到本机类型中。 此外，还将应用以下语义：

-   不以两个下划线（\_\_）开头的任何名称将显示在可视化效果中。

-   属于标准 JavaScript 对象的名称，或属于 JavaScript 提供程序创建的协议的一部分的名称将不会显示在可视化效果中。

-   可以通过 \[Symbol\]的支持使对象可迭代。

-   通过支持包含多个函数的自定义协议，可以使对象成为可索引的对象： getDimensionality、getValueAt 和（可选） setValueAt。

**本机和 JavaScript 对象桥**

JavaScript 与调试器的对象模型之间的桥梁是双向的。 本机对象可以传递到 JavaScript，JavaScript 对象可以传递到调试器的表达式计算器。 作为示例，请考虑在我们的脚本中添加以下方法：

```javascript
function multiplyBySeven(val)
{
    return val * 7;
}
```

此方法现在可在上面的示例 LINQ 查询中使用。 首先，我们加载 JavaScript 可视化。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\arrayVisualizer2.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\arrayVisualizer2.js'

0:000> dx @$myScript = Debugger.State.Scripts.arrayVisualizer2.Contents
```

然后，可以使用 multiplyBySeven 函数 inline，如下所示。

```dbgcmd
0:000> dx g_array1D.Select(@$myScript.multiplyBySeven),d
g_array1D.Select(@$myScript.multiplyBySeven),d                
    [0]              : 0
    [1]              : 7
    [2]              : 14
    [3]              : 21
    [4]              : 28
```

## <a name="span-idbreakpointsspanspan-idbreakpointsspanspan-idbreakpointsspanconditional-breakpoints-with-javascript"></a><span id="Breakpoints"></span><span id="breakpoints"></span><span id="BREAKPOINTS"></span>带有 JavaScript 的条件断点


命中断点后，可以使用 JavaScript 执行补充处理。 例如，脚本可用于检查其他运行时值，然后确定是否要自动继续执行代码或停止并执行其他手动调试。

有关使用断点的常规信息，请参阅[控制断点的方法](methods-of-controlling-breakpoints.md)。

**DebugHandler 示例断点处理脚本**

此示例将评估记事本的 "打开并保存" 对话框：*记事本！ShowOpenSaveDialog*。 此脚本将计算 pszCaption 变量，以确定当前的对话框是否为 "Open" 对话框或 "另存为" 对话框。 如果它是一个打开的对话框，则代码执行将继续。 如果它是 "另存为" 对话框，则代码执行将停止，并且调试器将在中中断。

```javascript
 // Use JavaScript strict mode 
"use strict";

// Define the invokeScript method to handle breakpoints

 function invokeScript()
 {
    var ctl = host.namespace.Debugger.Utility.Control;

    //Get the address of my string
    var address = host.evaluateExpression("pszCaption");

    // The open and save dialogs use the same function
    // When we hit the open dialog, continue.
    // When we hit the save dialog, break.
    if (host.memory.readWideString(address) == "Open") {
        // host.diagnostics.debugLog("We're opening, let's continue!\n");
        ctl.ExecuteCommand("gc");
    }
    else
    {
        //host.diagnostics.debugLog("We're saving, let's break!\n");
    }
  }
```

使用[**load （Load EXTENSION DLL）** ](-load---loadby--load-extension-dll-.md)命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

此命令在记事本上设置断点！ShowOpenSaveDialog，只要命中断点，就会运行上述脚本。

```dbgcmd
bp notepad!ShowOpenSaveDialog ".scriptrun C:\\WinDbg\\Scripts\\DebugHandler.js"
```

然后，在 "记事本" 中选择 "文件 &gt; 保存" 选项时，将运行该脚本，不发送 g 命令，并在执行代码时进行中断。

```dbgcmd
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\DebugHandler.js'
notepad!ShowOpenSaveDialog:
00007ff6`f9761884 48895c2408      mov     qword ptr [rsp+8],rbx ss:000000db`d2a9f2f0=0000021985fe2060
```

## <a name="span-idbitvaluesspanspan-idbitvaluesspanspan-idbitvaluesspanwork-with-64-bit-values-in-javascript-extensions"></a><span id="BitValues"></span><span id="bitvalues"></span><span id="BITVALUES"></span>使用 JavaScript 扩展中的64位值


本部分介绍如何将64位值传入 JavaScript 调试器扩展。 此问题是因为 JavaScript 只能使用53位存储数字。

**64位和 JavaScript 53 位存储**

传递给 JavaScript 的序号值通常作为 JavaScript 编号进行封送处理。 出现这种情况的问题是 JavaScript 号码为64位双精度浮点值。 超过53位的任何序号都将丢失进入 JavaScript 的精度。 这对于64位指针和其他可能具有最大字节标志的64位序号值提出了问题。 为了应对这种情况，可以输入 JavaScript 的任何64位本机值（无论是本机代码还是数据模型）都作为库类型输入，而不是作为 JavaScript 编号。 此库类型将往返回本机代码，而不会丢失数值精度。

**自动转换**

64位序号值的库类型支持标准 JavaScript valueOf 转换。 如果对象用于数学运算或其他需要值转换的构造中，它将自动转换为 JavaScript 数字。 如果发生精度损失（值使用超过53位的序号精度），JavaScript 提供程序将引发异常。

请注意，如果在 JavaScript 中使用位运算符，则会进一步限制为32位的序号精度。

此示例代码将两个数字相加，并将用于测试64位值的转换。

```javascript
function playWith64BitValues(a64, b64)
{
    // Sum two numbers to demonstrate 64-bit behavior.
    //
    // Imagine a64==100, b64==1000
    // The below would result in sum==1100 as a JavaScript number.  No exception is thrown.  The values auto-convert.
    //
    // Imagine a64==2^56, b64=1
    // The below will **Throw an Exception**.  Conversion to numeric results in loss of precision!
    //
    var sum = a64 + b64;
    host.diagnostics.debugLog("Sum   >> ", sum, "\n");

}

function performOp64BitValues(a64, b64, op)
{
    //
    // Call a data model method passing 64-bit value.  There is no loss of precision here.  This round trips perfectly.
    // For example:
    //  0:000> dx @$myScript.playWith64BitValues(0x4444444444444444ull, 0x3333333333333333ull, (x, y) => x + y)
    //  @$myScript.playWith64BitValues(0x4444444444444444ull, 0x3333333333333333ull, (x, y) => x + y) : 0x7777777777777777
    //
    return op(a64, b64);
}
```

使用文本编辑器（如记事本）创建名为*PlayWith64BitValues*的文本文件

使用[**load （Load EXTENSION DLL）** ](-load---loadby--load-extension-dll-.md)命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用 scriptload 命令加载脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\PlayWith64BitValues.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\PlayWith64BitValues.js'
```

为了更方便地使用该脚本，请在调试器中分配一个变量，以便使用 dx 命令保存该脚本的内容。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.PlayWith64BitValues.Contents
```

使用 dx 表达式计算器调用 addTwoValues 函数。

首先，我们将计算 "2 ^ 53 = 9007199254740992 （Hex 0x20000000000000）" 的值。

首先，我们将使用（2 ^ 53）-2，并查看它是否为 sum 返回正确的值。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740990)
Sum   >> 18014398509481980
```

接下来，我们将计算（2 ^ 53）-1 = 9007199254740991。 这会返回错误，指示转换过程会丢失精度，因此，这是可与 JavaScript 代码中的 sum 方法一起使用的最大值。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740991)
Error: 64 bit value loses precision on conversion to number
```

调用数据模型方法，传递64位值。 此处没有精度损失。

```dbgcmd
0:001> dx @$myScript.performOp64BitValues( 0x7FFFFFFFFFFFFFFF,  0x7FFFFFFFFFFFFFFF, (x, y) => x + y)
@$myScript.performOp64BitValues( 0x7FFFFFFFFFFFFFFF,  0x7FFFFFFFFFFFFFFF, (x, y) => x + y) : 0xfffffffffffffffe
```

**结果**

64位库类型是一个 JavaScript 对象，而不是一个值类型（如 JavaScript 编号）。 这对比较运算有一些影响。 通常，对象上的相等（= =）将指示操作数引用相同的对象，而不是相同的值。 JavaScript 提供程序通过跟踪对64位值的实时引用并为非收集的64位值返回相同的 "不可变" 对象来缓解这种情况。 这意味着，为了进行比较，将发生以下情况。

```javascript
// Comparison with 64 Bit Values

function comparisonWith64BitValues(a64, b64)
{
    //
    // No auto-conversion occurs here.  This is an *EFFECTIVE* value comparison.  This works with ordinals with above 53-bits of precision.
    //
    var areEqual = (a64 == b64);
    host.diagnostics.debugLog("areEqual   >> ", areEqual, "\n");
    var areNotEqual = (a64 != b64);
    host.diagnostics.debugLog("areNotEqual   >> ", areNotEqual, "\n");

    //
    // Auto-conversion occurs here.  This will throw if a64 does not pack into a JavaScript number with no loss of precision.
    //
    var isEqualTo42 = (a64 == 42);
    host.diagnostics.debugLog("isEqualTo42   >> ", isEqualTo42, "\n");
    var isLess = (a64 < b64);
    host.diagnostics.debugLog("isLess   >> ", isLess, "\n");
```

使用文本编辑器（如记事本）创建名为*ComparisonWith64BitValues*的文本文件

使用[**load （Load EXTENSION DLL）** ](-load---loadby--load-extension-dll-.md)命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用 scriptload 命令加载脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\ComparisonWith64BitValues.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\ComparisonWith64BitValues.js'
```

为了更方便地使用该脚本，请在调试器中分配一个变量，以便使用 dx 命令保存该脚本的内容。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.comparisonWith64BitValues.Contents
```

首先，我们将使用（2 ^ 53）-2，并查看它是否返回预期值。

```dbgcmd
0:001> dx @$myScript.comparisonWith64BitValues(9007199254740990, 9007199254740990)
areEqual   >> true
areNotEqual   >> false
isEqualTo42   >> false
isLess   >> false
```

我们还将尝试使用数字42作为第一个值来验证比较运算符是否正常工作。

```dbgcmd
0:001> dx @$myScript.comparisonWith64BitValues(42, 9007199254740990)
areEqual   >> false
areNotEqual   >> true
isEqualTo42   >> true
isLess   >> true
```

接下来，我们将计算（2 ^ 53）-1 = 9007199254740991。 此值返回错误，指示转换过程将丢失精度，因此这是可与 JavaScript 代码中的比较运算符一起使用的最大值。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740991)
Error: 64 bit value loses precision on conversion to number
```

**维护操作中的精度**

为了允许调试器扩展维护精度，一组数学函数将在64位库类型的顶层进行投影。 如果扩展需要（或可能）需要对传入64位值使用超过53位的精度，则应使用以下方法，而不是依赖标准运算符：

|                   |                           |                                                                                                               |
|-------------------|---------------------------|---------------------------------------------------------------------------------------------------------------|
| **方法名称**   | **信号**             | **描述**                                                                                               |
| asNumber          | .asNumber()               | 将64位值转换为 JavaScript 数字。 如果发生精度损失，则 \*\*引发异常\*\* |
| convertToNumber   | .convertToNumber()        | 将64位值转换为 JavaScript 数字。 如果发生精度损失，则 \*\*不会引发异常\*\* |
| getLowPart        | .getLowPart()             | 将64位值的低32位转换为 JavaScript 数字                                         |
| getHighPart       | .getHighPart()            | 将64位值的高32位转换为 JavaScript 数字                                          |
| add               | 。添加（值）               | 将一个值添加到64位值并返回结果                                                       |
| 减去          | . 减法（值）          | 从64位值中减去一个值并返回结果                                                |
| 乘          | 。乘（值）          | 用所提供的值乘以64位值并返回结果。                                      |
| 拆分            | 除数（值）            | 将64位值除以提供的值并返回结果                                         |
| bitwiseAnd        | . bitwiseAnd （值）        | 用提供的值计算64位值的按位 "与"，并返回结果                   |
| bitwiseOr         | . bitwiseOr （值）         | 用提供的值计算64位值的按位 "或"，并返回结果                    |
| bitwiseXor        | . bitwiseXor （值）        | 用提供的值计算64位值的按位 xor 并返回结果。                   |
| bitwiseShiftLeft  | . bitwiseShiftLeft （值）  | 将64位值向左移动给定的量并返回结果                                       |
| bitwiseShiftRight | . bitwiseShiftRight （值） | 将64位值向右移动给定的量并返回结果                                      |
| toString          | toString （\[基数\]）      | 将64位值转换为默认基数（或（可选）提供的基数）中的显示字符串         |



## <a name="span-iddebuggingspanspan-iddebuggingspanspan-iddebuggingspanjavascript-debugging"></a><span id="Debugging"></span><span id="debugging"></span><span id="DEBUGGING"></span>JavaScript 调试 

本部分介绍如何使用调试器的脚本调试功能。 调试程序已集成支持使用[. scriptdebug （调试 javascript）](-scriptdebug--debug-javascript-.md)命令调试 javascript 脚本。

>[!NOTE] 
> 若要对 WinDbg Preview 使用 JavaScript 调试，请以管理员身份运行调试器。
>


使用此示例代码可浏览 JavaScript 调试。 对于本演练，我们会将其命名为 DebuggableSample，并将其保存在 C:\MyScripts 目录中。

```javascript
"use strict";

class myObj
{
    toString()
    {
        var x = undefined[42];
        host.diagnostics.debugLog("BOO!\n");
    }
}

class iterObj
{
    *[Symbol.iterator]()
    {
        throw new Error("Oopsies!");
    }
}

function foo()
{
    return new myObj();
}

function iter()
{
    return new iterObj();
}

function throwAndCatch()
{
    var outer = undefined;
    var someObj = {a : 99, b : {c : 32, d: "Hello World"} };
    var curProc = host.currentProcess;
    var curThread = host.currentThread;

    try
    {
        var x = undefined[42];
    } catch(e) 
    {
        outer = e;
    }

    host.diagnostics.debugLog("This is a fun test\n");
    host.diagnostics.debugLog("Of the script debugger\n");
    var foo = {a : 99, b : 72};
    host.diagnostics.debugLog("foo.a = ", foo.a, "\n");

    return outer;
}

function throwUnhandled()
{
    var proc = host.currentProcess;
    var thread = host.currentThread;
    host.diagnostics.debugLog("Hello...  About to throw an exception!\n");
    throw new Error("Oh me oh my!  This is an unhandled exception!\n");
    host.diagnostics.debugLog("Oh...  this will never be hit!\n");
    return proc;
}

function outer()
{
    host.diagnostics.debugLog("inside outer!\n");
    var foo = throwAndCatch();
    host.diagnostics.debugLog("Caught and returned!\n");
    return foo;
}

function outermost()
{
    var x = 99;
    var result = outer();
    var y = 32;
    host.diagnostics.debugLog("Test\n");
    return result;
}

function initializeScript()
{
    //
    // Return an array of registration objects to modify the object model of the debugger
    // See the following for more details:
    //
    //     https://aka.ms/JsDbgExt
    //
}
```

加载示例脚本。

```dbgcmd
.scriptload C:\MyScripts\DebuggableSample.js
```

使用**scriptdebug**命令开始主动调试脚本。

```dbgcmd
0:000> .scriptdebug C:\MyScripts\DebuggableSample.js
>>> ****** DEBUGGER ENTRY DebuggableSample ******
           No active debug event!

>>> Debug [DebuggableSample <No Position>] >
```

看到提示后 *> > > 调试 [DebuggableSample <No Position>] >* 并请求输入请求，就是在脚本调试器内。  

使用 " **help** " 命令可显示 JavaScript 调试环境中的命令列表。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >.help
Script Debugger Commands (*NOTE* IDs are **PER SCRIPT**):
    ? .................................. Get help
    ? <expr>  .......................... Evaluate expression <expr> and display result
    ?? <expr>  ......................... Evaluate expression <expr> and display result
    |  ................................. List available scripts
    |<scriptid>s  ...................... Switch context to the given script
    bc <bpid>  ......................... Clear breakpoint by specified <bpid>
    bd <bpid>  ......................... Disable breakpoint by specified <bpid>
    be <bpid>  ......................... Enable breakpoint by specified <bpid>
    bl  ................................ List breakpoints
    bp <line>:<column>  ................ Set breakpoint at the specified line and column
    bp <function-name>  ................ Set breakpoint at the (global) function specified by the given name
    bpc  ............................... Set breakpoint at current location
    dv  ................................ Display local variables of current frame
    g  ................................. Continue script
    gu   ............................... Step out
    k  ................................. Get stack trace
    p  ................................. Step over
    q  ................................. Exit script debugger (resume execution)
    sx  ................................ Display available events/exceptions to break on
    sxe <event>  ....................... Enable break on <event>
    sxd <event>  ....................... Disable break on <event>
    t  ................................. Step in
    .attach <scriptId>  ................ Attach debugger to the script specified by <scriptId>
    .detach [<scriptId>]  .............. Detach debugger from the script specified by <scriptId>
    .frame <index>  .................... Switch to frame number <index>
    .f+  ............................... Switch to next stack frame
    .f-  ............................... Switch to previous stack frame
    .help  ............................. Get help
```

使用**sx** script 调试器命令可以查看我们可以捕获的事件列表。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sx              
sx                                                          
    ab  [   inactive] .... Break on script abort            
    eh  [   inactive] .... Break on any thrown exception    
    en  [   inactive] .... Break on entry to the script     
    uh  [     active] .... Break on unhandled exception     
```

使用**sxe** script 调试程序命令在进入时启用中断，以便脚本在其执行的任何代码执行时都将捕获到脚本调试器中。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sxe en          
sxe en                                                      
Event filter 'en' is now active                             
```


退出脚本调试器，我们将在脚本中调用将捕获到调试器中的脚本。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >q
```

此时，你将回到普通调试器。  执行以下命令以调用脚本。

```dbgcmd
dx @$scriptContents.outermost()
```

现在，你将回到脚本调试器，并将其放入最外层 JavaScript 函数的第一行。  

```dbgcmd
>>> ****** SCRIPT BREAK DebuggableSample [BreakIn] ******   
           Location: line = 73, column = 5                  
           Text: var x = 99                                 

>>> Debug [DebuggableSample 73:5] >                         
```

除了查看调试器中的断点外，还可以获取有关行（73）的信息以及发生中断的列（5）以及源代码的相关代码段： *var x = 99*。

接下来，我们将执行几次操作，并转到脚本中的其他位置。

```dbgcmd
    p
    t
    p
    t
    p
    p
```

此时，应在第34行中分解为 throwAndCatch 方法。  

```dbgcmd
...
>>> ****** SCRIPT BREAK DebuggableSample [Step Complete] ******                       
           Location: line = 34, column = 5                                            
           Text: var curProc = host.currentProcess                                    
```

可以通过执行堆栈跟踪来验证这一点。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

你可以从此处调查变量的值。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >??someObj                
??someObj                                                   
someObj          : {...}                                    
    __proto__        : {...}                                
    a                : 0x63                                 
    b                : {...}                                
>>> Debug [DebuggableSample 34:5] >??someObj.b              
??someObj.b                                                 
someObj.b        : {...}                                    
    __proto__        : {...}                                
    c                : 0x20                                 
    d                : Hello World                          
```

让我们在当前代码行上设置断点，并查看现在设置了哪些断点。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >bpc                      
bpc                                                         
Breakpoint 1 set at 34:5                                    
>>> Debug [DebuggableSample 34:5] >bl                       
bl                                                          
      Id State    Pos                                       
       1 enabled  34:5                                      
```

在这里，我们将使用**sxd** script 调试器命令禁用条目（en）事件。 

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >sxd en                                                                              
sxd en                                                                                                                 
Event filter 'en' is now inactive                                                                                      
```

然后，让脚本继续到末尾。

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >g                                                                                   
g                                                                                                                      
This is a fun test                                                                                                     
Of the script debugger                                                                                                 
foo.a = 99                                                                                                             
Caught and returned!                                                                                                   
Test                                                                                                                   
...
```

再次执行脚本方法，并查看命中断点。

```dbgcmd
0:000> dx @$scriptContents.outermost()                                                
inside outer!                                                                         
>>> ****** SCRIPT BREAK DebuggableSample [Breakpoint 1] ******                        
           Location: line = 34, column = 5                                            
           Text: var curProc = host.currentProcess                                    
```

显示调用堆栈。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

此时，我们想要停止调试此脚本，以便从该脚本中分离。  

```dbgcmd
>>> Debug [DebuggableSample 34:5] >.detach                  
.detach                                                     
Debugger has been detached from script!                     
```

然后键入 q 退出。

```dbgcmd                             
q                                                           
This is a fun test                                          
Of the script debugger                                      
foo.a = 99                                                  
Caught and returned!                                        
Test                                                        
```

再次执行函数将不再中断调试器。

```dbgcmd
0:007> dx @$scriptContents.outermost()
inside outer!
This is a fun test
Of the script debugger
foo.a = 99
Caught and returned!
Test
```

## <a name="span-idvscodespanspan-idvscodespanspan-idvscodespanjavascript-in-vscode---adding-intellisense"></a><span id="Vscode"></span><span id="vscode"></span><span id="VSCODE"></span>VSCode 中的 JavaScript-添加 IntelliSense

如果要在 VSCode 中使用调试器数据模型对象，则可以使用 Windows 开发工具包中提供的定义文件。 IntelliSense 定义文件为所有主机提供支持。 * 调试器对象 Api。 如果在64位计算机上的默认目录中安装了工具包，则该工具包位于以下位置：

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext\JsProvider.d.ts`

若要在 VSCode 中使用 IntelliSense 定义文件：

1. 找到定义文件-JSProvider

2. 将定义文件复制到与脚本相同的文件夹中。

3. 将 `/// <reference path="JSProvider.d.ts" />` 添加到 JavaScript 脚本文件的顶部。

使用 JavaScript 文件中的该引用，VS Code 将自动为你提供 JSProvider 提供的宿主 Api 上的 IntelliSense，以及脚本中的结构。 例如，键入 "host"。 你将看到所有可用调试器模型 Api 的 IntelliSense。


## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspanjavascript-resources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>JavaScript 资源


下面是开发 JavaScript 调试扩展时可能会有用的 JavaScript 资源。

-   [编写 JavaScript 代码](https://docs.microsoft.com/scripting/javascript/writing-javascript-code)

-   [JScript 语言教程](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/t895bwkh(v=vs.100))

-   [Mozilla JavaScript 参考](https://developer.mozilla.org/docs/Web/JavaScript)

-   [WinJS： Windows JavaScript 库](https://github.com/winjs/winjs)

-   [ECMAScript 6-新增功能：概述 & 比较](https://es6-features.org/)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[JavaScript 调试器示例脚本](javascript-debugger-example-scripts.md)

[JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)











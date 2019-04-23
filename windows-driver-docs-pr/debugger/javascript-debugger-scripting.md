---
title: JavaScript 调试器脚本
description: 本主题介绍如何使用 JavaScript 创建脚本，了解调试器对象和扩展和自定义调试器的功能。
ms.assetid: 3442E2C4-4054-4698-B7FB-8FE19D26C171
ms.date: 04/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: ab8a09abb89ace35b8d44b6f1356432d73d860b4
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902473"
---
# <a name="javascript-debugger-scripting"></a>JavaScript 调试器脚本


本主题介绍如何使用 JavaScript 创建脚本，了解调试器对象和扩展和自定义调试器的功能。

## <a name="span-idoverviewofjavascriptdebuggerscriptingspanspan-idoverviewofjavascriptdebuggerscriptingspanspan-idoverviewofjavascriptdebuggerscriptingspanoverview-of-javascript-debugger-scripting"></a><span id="Overview_of_JavaScript_Debugger_Scripting_"></span><span id="overview_of_javascript_debugger_scripting_"></span><span id="OVERVIEW_OF_JAVASCRIPT_DEBUGGER_SCRIPTING_"></span>脚本编写的 JavaScript 调试器的概述


脚本提供程序起到调试器的内部对象模型脚本语言。 JavaScript 调试器脚本编写提供程序，允许以 JavaScript 用于调试程序。

通过.scriptload 命令加载 JavaScript 时，执行该脚本的根代码、 在脚本中提供的名称被桥接至调试程序 (dx 调试程序) 的根命名空间和在卸载之后，该脚本一直驻留在内存中和将释放对它的对象的所有引用。 该脚本可以提供新功能到调试器的表达式计算器，修改的对象模型的调试器，或可充当可视化工具在很大程度的相同的 NatVis 可视化工具的方式处理。

本主题介绍了一些可以使用脚本编写的 JavaScript 调试器执行的操作。

[加载调试器 JavaScript 提供程序](#provider)

[使用 JavaScript 脚本元命令](#commands)

[开始使用脚本编写的 JavaScript 调试器](#started)

[自动执行调试器命令](#automate)

[使用 JavaScript 设置条件断点](#breakpoints)

[在 JavaScript 中创建调试器可视化工具](#visualizer)

[使用 JavaScript 扩展中的 64 位值](#bitvalues)

[JavaScript 调试](#debugging)

[VSCode-添加 IntelliSense 中的 JavaScript](#vscode)

[JavaScript 资源](#resources)

这两个主题提供有关如何使用 JavaScript 在调试器中的其他信息。

[JavaScript 调试器的示例脚本](javascript-debugger-example-scripts.md)

[JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)


## <a name="javascript-scripting-video"></a>JavaScript 脚本视频

[碎片整理工具 #170](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-170-Debugger-JavaScript-Scripting) -Andy 和帐单演示 JavaScript 可扩展性和脚本编写在调试器中的功能。


## <a name="span-idproviderspanspan-idproviderspanspan-idproviderspanthe-debugger-javascript-provider"></a><span id="Provider"></span><span id="provider"></span><span id="PROVIDER"></span>调试器 JavaScript 提供程序

附带调试器的 JavaScript 提供程序可以完全利用的最新 ECMAScript6 对象和类增强功能。 有关详细信息，请参阅[ECMAScript 6-新功能：概述和比较](https://es6-features.org/)。

**JsProvider.dll**

JsProvider.dll 是加载来支持 JavaScript 调试器脚本编写的 JavaScript 提供程序。

**要求**

JavaScript 调试器脚本设计用于所有支持的 Windows 版本。

## <a name="span-idloadingthejavascriptscriptingproviderspanspan-idloadingthejavascriptscriptingproviderspanspan-idloadingthejavascriptscriptingproviderspanloading-the-javascript-scripting-provider"></a><span id="Loading_the_JavaScript_Scripting_Provider"></span><span id="loading_the_javascript_scripting_provider"></span><span id="LOADING_THE_JAVASCRIPT_SCRIPTING_PROVIDER"></span>加载脚本编写提供程序的 JavaScript


在使用之前的任何.script 命令，脚本编写提供程序需要使用加载[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令。 若要加载的 JavaScript 提供程序，请使用以下命令。

```dbgcmd
0:000> .load jsprovider.dll
```

使用.scriptproviders 命令来确认已加载的 JavaScript 提供程序。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

## <a name="span-idcommandsspanspan-idcommandsspanspan-idcommandsspanjavascript-scripting-meta-commands"></a><span id="Commands"></span><span id="commands"></span><span id="COMMANDS"></span>JavaScript 脚本元命令


以下命令是可用于使用 JavaScript 调试器编写脚本。

-   [**.scriptproviders （列表脚本提供程序）**](-scriptproviders--list-script-providers-.md)
-   [**.scriptload （负载脚本）**](-scriptload--load-script-.md)
-   [**.scriptunload （卸载脚本）**](-scriptunload--unload-script-.md)
-   [**.scriptrun （运行脚本）**](-scriptrun--run-script-.md)
-   [**.scriptlist （列出已加载的脚本）**](-scriptlist--list-loaded-scripts-.md)

**要求**

在使用之前的任何.script 命令，脚本编写提供程序需要使用加载[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令。 若要加载的 JavaScript 提供程序，请使用以下命令。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idscriptproviderslistscriptprovidersspanspan-idscriptproviderslistscriptprovidersspanscriptproviders-list-script-providers"></a><span id=".scriptproviders__list_script_providers_"></span><span id=".SCRIPTPROVIDERS__LIST_SCRIPT_PROVIDERS_"></span>.scriptproviders （列表脚本提供程序）


.Scriptproviders 命令将列出其目前能够理解的调试器，并在其下它们要注册的扩展的脚本语言。

在下面的示例中，将加载的 JavaScript 和 NatVis 提供程序。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

以结尾的任何文件"。NatVis"理解为 NatVis 脚本并以".js"结尾的任何文件理解为 JavaScript 脚本。 可以使用.scriptload 命令加载任一类型的脚本。

有关详细信息，请参阅[ **.scriptproviders （列表脚本提供程序）**](-scriptproviders--list-script-providers-.md)

## <a name="span-idscriptloadloadscriptspanspan-idscriptloadloadscriptspanscriptload-load-script"></a><span id=".scriptload__load_script_"></span><span id=".SCRIPTLOAD__LOAD_SCRIPT_"></span>.scriptload （负载脚本）


.Scriptload 命令将加载脚本并执行脚本的根代码和*initializeScript*函数。 如果在初始加载和执行脚本中的任何错误，错误将显示到控制台。 下面的命令演示 TestScript.js 成功加载。

```dbgcmd
0:000> .scriptload C:\WinDbg\Scripts\TestScript.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\TestScript.js'
```

脚本所做的任何对象模型操作将就地保留，直到该脚本随后卸载或重新运行具有不同的内容。

有关详细信息，请参阅[ **.scriptload （负载脚本）**](-scriptload--load-script-.md)

## <a name="span-idscriptrunspanscriptrun"></a><span id=".SCRIPTRUN"></span>.scriptrun


.Scriptrun 命令将加载脚本，请执行该脚本的根代码*initializeScript*并*invokeScript*函数。 如果在初始加载和执行脚本中的任何错误，错误将显示到控制台。

```dbgcmd
0:000> .scriptrun C:\WinDbg\Scripts\helloWorld.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\helloWorld.js'
Hello World!  We are in JavaScript!
```

脚本所做的任何调试器对象模型操作将就地保留，直到该脚本随后卸载或重新运行具有不同的内容。

有关详细信息，请参阅[ **.scriptrun （运行脚本）**](-scriptrun--run-script-.md)。

## <a name="span-idscriptunloadunloadscriptspanspan-idscriptunloadunloadscriptspanscriptunload-unload-script"></a><span id=".scriptunload__unload_script_"></span><span id=".SCRIPTUNLOAD__UNLOAD_SCRIPT_"></span>.scriptunload （卸载脚本）


.Scriptunload 命令卸载加载的脚本并调用*uninitializeScript*函数。 使用以下命令语法来卸载脚本

```dbgcmd
0:000:x86> .scriptunload C:\WinDbg\Scripts\TestScript.js
JavaScript script unloaded from 'C:\WinDbg\Scripts\TestScript.js'
```

有关详细信息，请参阅[ **.scriptunload （卸载脚本）**](-scriptunload--unload-script-.md)。

## <a name="span-idscriptlistlistloadedscriptsspanspan-idscriptlistlistloadedscriptsspanscriptlist-list-loaded-scripts"></a><span id=".scriptlist__list_loaded_scripts_"></span><span id=".SCRIPTLIST__LIST_LOADED_SCRIPTS_"></span>.scriptlist （列出已加载的脚本）


.Scriptlist 命令将列出已加载通过.scriptload 或.scriptrun 命令的任何脚本。 如果 TestScript 已成功加载使用.scriptload，.scriptlist 命令将显示加载的脚本的名称。

```dbgcmd
0:000> .scriptlist
Command Loaded Scripts:
    JavaScript script from 'C:\WinDbg\Scripts\TestScript.js'
```

有关详细信息，请参阅[ **.scriptlist （列表加载脚本）**](-scriptlist--list-loaded-scripts-.md)。

## <a name="span-idstartedspanspan-idstartedspanspan-idstartedspanget-started-with-javascript-debugger-scripting"></a><span id="Started"></span><span id="started"></span><span id="STARTED"></span>开始使用脚本编写的 JavaScript 调试器


### <a name="span-idhelloworldexamplescriptspanspan-idhelloworldexamplescriptspanspan-idhelloworldexamplescriptspanhelloworld-example-script"></a><span id="HelloWorld_Example_Script"></span><span id="helloworld_example_script"></span><span id="HELLOWORLD_EXAMPLE_SCRIPT"></span>HelloWorld 示例脚本

本部分介绍如何创建和执行打印出 Hello World 的简单 JavaScript 调试器脚本。

```dbgcmd
// WinDbg JavaScript sample
// Prints Hello World
function initializeScript()
{
    host.diagnostics.debugLog("***> Hello World! \n");
}
```

使用记事本等文本编辑器创建一个名为文本文件*HelloWorld.js* ，其中包含上面所示的 JavaScript 代码。

使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用.scriptload 命令加载并执行脚本。 因为我们使用了函数名称*initializeScript*，该函数中的代码运行时加载该脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\HelloWorld.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\HelloWorld.js'
***> Hello World! 
```

加载脚本之后的其他功能是在调试器中可用。 使用[ **dx （显示 NatVis 表达式）** ](dx--display-visualizer-variables-.md)命令以显示*Debugger.State.Scripts*以查看我们的脚本现在驻留。

```dbgcmd
0:000> dx Debugger.State.Scripts
Debugger.State.Scripts                
    HelloWorld 
```

在下一步的示例中，我们将添加，并调用命名的函数。

### <a name="span-idaddingtwovaluesexamplescriptspanspan-idaddingtwovaluesexamplescriptspanspan-idaddingtwovaluesexamplescriptspanadding-two-values-example-script"></a><span id="Adding_Two_Values_Example_Script"></span><span id="adding_two_values_example_script"></span><span id="ADDING_TWO_VALUES_EXAMPLE_SCRIPT"></span>添加两个值的示例脚本

本部分介绍如何创建和执行简单的 JavaScript 调试器中添加的脚本采用输入，并添加两个数字。

这个简单的脚本提供了一个函数，addTwoValues。

```dbgcmd
// WinDbg JavaScript sample
// Adds two functions
function addTwoValues(a, b)
 {
     return a + b;
 }
```

使用记事本等文本编辑器创建一个名为文本文件*FirstSampleFunction.js*

使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用.scriptload 命令加载该脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\FirstSampleFunction.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\FirstSampleFunction.js'
```

加载脚本之后的其他功能是在调试器中可用。 使用[ **dx （显示 NatVis 表达式）** ](dx--display-visualizer-variables-.md)命令以显示*Debugger.State.Scripts*以查看我们的脚本现在驻留。

```dbgcmd
0:000> dx Debugger.State.Scripts
Debugger.State.Scripts                
    FirstSampleFunction    
```

我们可以单击*FirstSampleFunction*，以查看它提供了哪些功能。

```dbgcmd
0:000> dx -r1 -v Debugger.State.Scripts.FirstSampleFunction.Contents
Debugger.State.Scripts.FirstSampleFunction.Contents                 : [object Object]
    host             : [object Object]
    addTwoValues    
 ... 
```

若要使脚本更方便地使用，分配用于保存使用 dx 命令脚本的内容在调试器中的变量。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.FirstSampleFunction.Contents
```

使用 dx 表达式计算器调用 addTwoValues 函数。

```dbgcmd
0:000> dx @$myScript.addTwoValues(10, 41),d
@$myScript.addTwoValues(10, 41),d : 51
```

此外可以使用 *@$ scriptContents*内置的别名来处理脚本。 *@$ ScriptContents*别名将合并所有。所有已加载的脚本的内容。

```dbgcmd
0:001> dx @$scriptContents.addTwoValues(10, 40),d
@$scriptContents.addTwoValues(10, 40),d : 50
```

完成后使用该脚本使用.scriptunload 命令卸载脚本。

```dbgcmd
0:000> .scriptunload c:\WinDbg\Scripts\FirstSampleFunction.js
JavaScript script successfully unloaded from 'c:\WinDbg\Scripts\FirstSampleFunction.js'
```

### <a name="span-idautomatespanspan-idautomatespanspan-idautomatespandebugger-command-automation"></a><span id="Automate"></span><span id="automate"></span><span id="AUTOMATE"></span>调试器命令自动化

本部分介绍如何创建和执行一个简单的 JavaScript 调试器脚本，用于自动执行的发送[ **u （反汇编）** ](u--unassemble-.md)命令。 该示例还演示如何收集和显示命令输出在循环中。

此脚本提供了一个函数，RunCommands()。

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

使用记事本等文本编辑器创建一个名为文本文件*RunCommands.js*

使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用.scriptload 命令加载 RunCommands 脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\RunCommands.js 
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\RunCommands.js'
```

加载脚本之后的其他功能是在调试器中可用。 使用[ **dx （显示 NatVis 表达式）** ](dx--display-visualizer-variables-.md)命令以显示*Debugger.State.Scripts.RunCommands*以查看我们的脚本现在驻留。

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

使用 dx 命令 RunCommands 函数 RunCommands 脚本中调用。

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

## <a name="span-idspecialjavascriptdebuggerfunctionsspanspan-idspecialjavascriptdebuggerfunctionsspanspan-idspecialjavascriptdebuggerfunctionsspanspecial-javascript-debugger-functions"></a><span id="Special_JavaScript_Debugger_Functions"></span><span id="special_javascript_debugger_functions"></span><span id="SPECIAL_JAVASCRIPT_DEBUGGER_FUNCTIONS"></span>特殊 JavaScript 调试器函数


在 JavaScript 脚本调用的脚本提供程序本身中有多个特殊函数。

### <a name="span-idinitializescriptspanspan-idinitializescriptspanspan-idinitializescriptspaninitializescript"></a><span id="initializeScript"></span><span id="initializescript"></span><span id="INITIALIZESCRIPT"></span>initializeScript

JavaScript 脚本加载和是执行，它将遍历一系列的步骤之前的变量，函数，并在脚本中的其他对象时影响的对象模型的调试器。

-   该脚本加载到内存并分析。
-   执行该脚本中的根代码。
-   如果脚本具有一个名为 initializeScript 方法，调用该方法。
-   InitializeScript 的返回值用于确定如何自动修改的对象模型的调试器。
-   在脚本中的名称被桥接到调试器的命名空间。

如前文所述，将执行该脚本的根代码后将立即调用 initializeScript。 其工作是，该值指示如何修改调试器的对象模型的提供程序返回的对象注册 JavaScript 数组。

```javascript
function initializeScript()
{
    // Add code here that you want to run every time the script is loaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> initializeScript was called\n");
}
```

### <a name="span-idinvokescriptspanspan-idinvokescriptspanspan-idinvokescriptspaninvokescript"></a><span id="invokeScript"></span><span id="invokescript"></span><span id="INVOKESCRIPT"></span>invokeScript

InvokeScript 方法是主脚本的方法，并运行.scriptload 和.scriptrun 时调用。

```javascript
function invokeScript()
{
    // Add code here that you want to run every time the script is executed. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> invokeScript was called\n");
}
```

### <a name="span-iduninitializescriptspanspan-iduninitializescriptspanspan-iduninitializescriptspanuninitializescript"></a><span id="uninitializeScript"></span><span id="uninitializescript"></span><span id="UNINITIALIZESCRIPT"></span>uninitializeScript

UninitializeScript 方法与 initializeScript 行为相反。 调用脚本的链接和已准备好卸载时。 它的工作是以撤消对对象模型的脚本在执行期间以强制方式进行任何更改和/或销毁任何对象的脚本缓存。

如果脚本既不使对象模型的命令性操作，也不会缓存结果，它不需要具有 uninitializeScript 方法。 对执行由 initializeScript 的返回值的对象模型的任何更改时将自动撤消该提供程序。 此类更改不需要显式 uninitializeScript 方法。

```javascript
function uninitializeScript()
{
    // Add code here that you want to run every time the script is unloaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> uninitialize was called\n");
}
```

## <a name="span-idsummaryoffunctionscalledbyscriptcommandsspanspan-idsummaryoffunctionscalledbyscriptcommandsspanspan-idsummaryoffunctionscalledbyscriptcommandsspansummary-of-functions-called-by-script-commands"></a><span id="Summary_of_Functions_Called_by_Script_Commands"></span><span id="summary_of_functions_called_by_script_commands"></span><span id="SUMMARY_OF_FUNCTIONS_CALLED_BY_SCRIPT_COMMANDS"></span>调用的函数的脚本命令的摘要


此表总结了由脚本命令调用的函数

||[.scriptload](-scriptload--load-script-.md)|[.scriptrun (Run Script)](-scriptrun--run-script-.md)|[.scriptunload （卸载脚本）](-scriptunload--unload-script-.md)|
|--- |--- |--- |--- |
|根|是|是| | |
|initializeScript|是|是| | |
|invokeScript       | |是| |
|uninitializeScript | ||是|


使用此示例代码以查看时就每个函数，如加载、 执行和卸载脚本。

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


自定义可视化效果文件，进行分组和组织更好地反映数据关系和内容的可视化结构中的数据。 JavaScript 调试器扩展可用于编写的方式非常类似于 NatVis 调试器可视化工具执行操作的。 通过创作一个 JavaScript 原型对象 （或 ES6 类） 它可充当给定数据的可视化工具类型完成此操作。 有关 NatVis 和调试器的详细信息请参阅[ **dx （显示 NatVis 表达式）**](dx--display-visualizer-variables-.md)。

**示例类-Simple1DArray**

考虑的一个示例C++类表示一维数组。 此类具有两个成员，m\_大小的数组和 m 的总体大小\_pValues 这是指向的内存中的整数数目等于 m\_大小字段。

```cpp
class Simple1DArray
{
private:

    ULONG64 m_size;
    int *m_pValues;
};
```

我们可以使用 dx 命令来查看默认数据结构呈现。

```dbgcmd
0:000> dx g_array1D
g_array1D                 [Type: Simple1DArray]
    [+0x000] m_size           : 0x5 [Type: unsigned __int64]
    [+0x008] m_pValues        : 0x8be32449e0 : 0 [Type: int *]
```

**JavaScript 可视化工具**

若要直观显示此类型，我们需要到作者的原型 （或 ES6） 类，该类包含所有字段和我们希望调试器显示属性。 我们还需要使 initializeScript 方法返回的对象，它指示要为给定类型的可视化工具链接我们原型的 JavaScript 提供程序。

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

将脚本保存在一个名为 arrayVisualizer.js 文件中。

使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

使用.scriptload 加载数组可视化工具脚本。

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

此外，此 JavaScript 可视化对象提供了 LINQ 功能，如 Select。

```dbgcmd
0:000> dx g_array1D.Select(n => n * 3),d
g_array1D.Select(n => n * 3),d                
    [0]              : 0
    [1]              : 3
    [2]              : 6
    [3]              : 9
    [4]              : 12
```

**什么会影响在可视化效果**

原型或发出时通过从 initializeScript host.typeSignatureRegistration 对象返回的本机类型可视化工具的类将具有的所有属性和方法在 JavaScript 中的添加到本机类型。 此外，将应用以下语义：

-   这不会启动两个下划线开头的任何名称 (\_\_) 可在可视化效果中。

-   这是标准的 JavaScript 对象的一部分或属于 JavaScript 提供程序创建的协议的名称都不会显示在可视化效果中。

-   对象可通过支持的可迭代\[Symbol.iterator\]。

-   对象可通过几个函数组成的自定义协议的支持可编制索引： getDimensionality，getValueAt，并根据需要 setValueAt。

**本机和 JavaScript 对象桥**

JavaScript 和调试程序的对象模型之间的桥是双向的。 本机对象可以传递到 JavaScript 和 JavaScript 对象可以传递到调试器的表达式计算器。 此示例，请考虑在我们的脚本的以下方法添加：

```javascript
function multiplyBySeven(val)
{
    return val * 7;
}
```

现在可以在上面的示例 LINQ 查询中利用此方法。 首先，我们将加载 JavaScript 可视化效果。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\arrayVisualizer2.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\arrayVisualizer2.js'

0:000> dx @$myScript = Debugger.State.Scripts.arrayVisualizer2.Contents
```

然后，可以使用 multiplyBySeven 函数内联，如下所示。

```dbgcmd
0:000> dx g_array1D.Select(@$myScript.multiplyBySeven),d
g_array1D.Select(@$myScript.multiplyBySeven),d                
    [0]              : 0
    [1]              : 7
    [2]              : 14
    [3]              : 21
    [4]              : 28
```

## <a name="span-idbreakpointsspanspan-idbreakpointsspanspan-idbreakpointsspanconditional-breakpoints-with-javascript"></a><span id="Breakpoints"></span><span id="breakpoints"></span><span id="BREAKPOINTS"></span>使用 JavaScript 的条件断点


可以使用 JavaScript 进行补充的处理后命中断点。 例如，可以使用脚本来检查运行的时的其他值，然后确定你是否想要自动继续执行代码或停止，并执行其他手动调试。

有关使用断点的常规信息，请参阅[控制断点方法](methods-of-controlling-breakpoints.md)。

**DebugHandler.js 示例断点处理脚本**

此示例将计算记事本的打开，并保存对话框：*记事本 ！ShowOpenSaveDialog*。 此脚本将评估 pszCaption 变量来确定是否当前对话框是"打开"对话框，或如果它是一个"另存为"对话框。 如果它是打开的对话框中，将继续执行代码。 如果它是另存为对话框中，将停止执行代码，并调试程序中断。

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

使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

此命令设置断点，在记事本 ！ShowOpenSaveDialog，并将运行上述脚本，每当命中该断点。

```dbgcmd
bp notepad!ShowOpenSaveDialog ".scriptrun C:\\WinDbg\\Scripts\\DebugHandler.js"
```

然后当文件&gt;记事本中选择保存选项、 运行脚本、 g 命令不会发送，和发生中断代码执行过程中的。

```dbgcmd
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\DebugHandler.js'
notepad!ShowOpenSaveDialog:
00007ff6`f9761884 48895c2408      mov     qword ptr [rsp+8],rbx ss:000000db`d2a9f2f0=0000021985fe2060
```

## <a name="span-idbitvaluesspanspan-idbitvaluesspanspan-idbitvaluesspanwork-with-64-bit-values-in-javascript-extensions"></a><span id="BitValues"></span><span id="bitvalues"></span><span id="BITVALUES"></span>使用 JavaScript 扩展中的 64 位值


本部分介绍如何使用 64 位值传递到 JavaScript 调试器扩展的行为。 因为 JavaScript 仅具有存储使用 53 位数字的功能，会出现此问题。

**64 位和 JavaScript 53 位存储**

为 JavaScript 数字通常封送到 JavaScript 传递的序号值。 与此问题是，JavaScript 数字均为 64 位双精度浮点值。 53 位任何序号可能会损失精度在 JavaScript 中的条目。 这会带来的 64 位指针和其他 64 位序号值可能包含标志以最高字节为单位的问题。 为了解决此问题，任何 64 位本机值 （无论是从本机代码或数据模型） 输入 JavaScript 输入作为库类型-不为一个 JavaScript 数字。 此库类型将返回到本机代码的往返过程而不会丢失数值精度。

**Auto-Conversion**

64 位的序数值的库类型支持的标准 JavaScript valueOf 转换。 如果在某个数学运算或其他构造这要求值的转换中使用的对象，它将自动转换为 JavaScript 数字。 出现精度降低时 （该值使用超过 53 位序号精度），JavaScript 提供程序将引发异常。

请注意，如果在 JavaScript 中使用按位运算符，您进一步限制为 32 位的序号的精度。

此代码示例两个数字相加并将用于测试 64 位值的转换。

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

使用记事本等文本编辑器创建一个名为文本文件*PlayWith64BitValues.js*

使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用.scriptload 命令加载该脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\PlayWith64BitValues.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\PlayWith64BitValues.js'
```

若要使脚本更方便地使用，分配用于保存使用 dx 命令脚本的内容在调试器中的变量。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.PlayWith64BitValues.Contents
```

使用 dx 表达式计算器调用 addTwoValues 函数。

首先，我们将计算的值为 2 ^53 = 9007199254740992 （十六进制 0x20000000000000）。

第一次测试，我们将使用 (2 ^53)-2，并查看它为 sum 返回正确的值。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740990)
Sum   >> 18014398509481980
```

然后我们将计算 (2 ^53)-1 = 9007199254740991。 这将返回错误，指出，转换过程将会丢失精度，因此，这是可以在 JavaScript 代码中的 sum 方法一起使用的最大值。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740991)
Error: 64 bit value loses precision on conversion to number
```

调用数据模型方法将 64 位值传递。 不会丢失任何精度此处。

```dbgcmd
0:001> dx @$myScript.performOp64BitValues( 0x7FFFFFFFFFFFFFFF,  0x7FFFFFFFFFFFFFFF, (x, y) => x + y)
@$myScript.performOp64BitValues( 0x7FFFFFFFFFFFFFFF,  0x7FFFFFFFFFFFFFFF, (x, y) => x + y) : 0xfffffffffffffffe
```

**Comparison**

64 位库类型为 JavaScript 对象并不像一个 JavaScript 数字的值类型。 这会影响某些比较操作。 通常情况下，对某个对象的相等 （= =） 将指示的操作数引用同一对象而不是相同的值。 JavaScript 提供程序可缓解这通过跟踪对 64 位值的实时引用并返回非收集 64 位的值相同"不可变"的对象。 这意味着为进行比较，下面会出现。

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

使用记事本等文本编辑器创建一个名为文本文件*ComparisonWith64BitValues.js*

使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

使用.scriptload 命令加载该脚本。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\ComparisonWith64BitValues.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\ComparisonWith64BitValues.js'
```

若要使脚本更方便地使用，分配用于保存使用 dx 命令脚本的内容在调试器中的变量。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.comparisonWith64BitValues.Contents
```

第一次测试，我们将使用 (2 ^53)-2，并查看它是否返回预期值。

```dbgcmd
0:001> dx @$myScript.comparisonWith64BitValues(9007199254740990, 9007199254740990)
areEqual   >> true
areNotEqual   >> false
isEqualTo42   >> false
isLess   >> false
```

我们还将重数为 42 所要验证的比较运算符的第一个值工作正常。

```dbgcmd
0:001> dx @$myScript.comparisonWith64BitValues(42, 9007199254740990)
areEqual   >> false
areNotEqual   >> true
isEqualTo42   >> true
isLess   >> true
```

然后我们将计算 (2 ^53)-1 = 9007199254740991。 此值返回错误，指出，转换过程将会丢失精度，因此，这是可以在 JavaScript 代码中的比较运算符的最大值。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740991)
Error: 64 bit value loses precision on conversion to number
```

**维护操作中的精度**

若要允许调试器扩展来维护精度，数学函数的一组被投影在 64 位库类型之上。 如果扩展需要 （或可能是可能） 需要上面 53 位精度的传入的 64 位值，而不是依靠标准运算符应利用以下方法：

|                   |                           |                                                                                                               |
|-------------------|---------------------------|---------------------------------------------------------------------------------------------------------------|
| **方法名称**   | **签名**             | **说明**                                                                                               |
| asNumber          | .asNumber()               | 64 位值转换为 JavaScript 数字。 发生精度损失时， \*\*会引发异常\*\* |
| convertToNumber   | .convertToNumber()        | 64 位值转换为 JavaScript 数字。 发生精度损失时， \*\*不会引发异常\*\* |
| getLowPart        | .getLowPart()             | 将 64 位值的低 32 位转换为 JavaScript 数字                                         |
| getHighPart       | .getHighPart()            | 将 64 位值的高 32 位转换为 JavaScript 数字                                          |
| 添加               | .add(value)               | 将值添加到 64 位值并返回结果                                                       |
| 相减          | .subtract(value)          | 从 64 位值减去的值并返回结果                                                |
| 相乘          | .multiply(value)          | 用提供的值的 64 位值乘以并返回结果                                      |
| 除            | .divide(value)            | 将 64 位值提供的值除以并返回结果                                         |
| bitwiseAnd        | .bitwiseAnd(value)        | 计算按位和 64 位值与提供的值的并返回结果                   |
| bitwiseOr         | .bitwiseOr(value)         | 计算按位或 64 位值与提供的值的并返回结果                    |
| bitwiseXor        | .bitwiseXor(value)        | 计算使用提供的值的 64 位值的按位 xor，并返回结果                   |
| bitwiseShiftLeft  | .bitwiseShiftLeft(value)  | 右移保留按给定数量的 64 位值并返回结果                                       |
| bitwiseShiftRight | .bitwiseShiftRight(value) | 将 64 位值向右移动按给定数量并返回结果                                      |
| toString          | .toString(\[radix\])      | 将 64 位值转换为默认基数 （或根据需要提供的基数） 中的显示字符串         |



## <a name="span-iddebuggingspanspan-iddebuggingspanspan-iddebuggingspanjavascript-debugging"></a><span id="Debugging"></span><span id="debugging"></span><span id="DEBUGGING"></span>JavaScript 调试 

本部分介绍如何使用脚本调试在调试器的功能。 调试器已集成支持使用 JavaScript 脚本进行调试[.scriptdebug (调试 JavaScript)](-scriptdebug--debug-javascript-.md)命令。

>[!NOTE] 
> 若要使用 JavaScript 调试 WinDbg 预览，请以管理员身份运行调试器。
>


此示例代码用于浏览调试 JavaScript。 对于本演练，我们将其命名为 DebuggableSample.js 并将其保存在 C:\MyScripts 目录中。

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

启动脚本使用主动进行调试 **.scriptdebug**命令。

```dbgcmd
0:000> .scriptdebug C:\MyScripts\DebuggableSample.js
>>> ****** DEBUGGER ENTRY DebuggableSample ******
           No active debug event!

>>> Debug [DebuggableSample <No Position>] >
```

一旦你会看到提示 *>>> 调试 [DebuggableSample <No Position>] >* 和输入的请求，则位于脚本调试器。  

使用 **.help 获取**命令以 JavaScript 调试环境中显示的命令的列表。

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

使用**sx**脚本调试器命令以查看事件列表我们可以捕获。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sx              
sx                                                          
    ab  [   inactive] .... Break on script abort            
    eh  [   inactive] .... Break on any thrown exception    
    en  [   inactive] .... Break on entry to the script     
    uh  [     active] .... Break on unhandled exception     
```

使用**sxe**脚本调试器命令，以便该脚本将捕获到脚本调试器中它的任何代码执行时，就立即开启条目上中断。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sxe en          
sxe en                                                      
Event filter 'en' is now active                             
```


退出脚本调试程序，我们将进行函数调用到将捕获到调试器的脚本。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >q
```

此时，你已返回标准调试器。  执行以下命令来调用脚本。

```dbgcmd
dx @$scriptContents.outermost()
```

现在，你已返回脚本调试程序并在最外面的 JavaScript 函数的第一行上中断。  

```dbgcmd
>>> ****** SCRIPT BREAK DebuggableSample [BreakIn] ******   
           Location: line = 73, column = 5                  
           Text: var x = 99                                 

>>> Debug [DebuggableSample 73:5] >                         
```

除了中断到调试器，获取行 (73) 和位置中断执行位置，以及源代码的相关代码段的列 (5) 的信息： *var x = 99*。

让我们来单步几次，转到脚本中的另一个位置。

```dbgcmd
    p
    t
    p
    t
    p
    p
```

此时，您应分解为多行 34 throwAndCatch 方法。  

```dbgcmd
...
>>> ****** SCRIPT BREAK DebuggableSample [Step Complete] ******                       
           Location: line = 34, column = 5                                            
           Text: var curProc = host.currentProcess                                    
```

可以通过执行堆栈跟踪对此进行验证。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

在这里，可以调查变量的值。

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

我们在当前代码行上设置断点，看现在设置哪些断点。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >bpc                      
bpc                                                         
Breakpoint 1 set at 34:5                                    
>>> Debug [DebuggableSample 34:5] >bl                       
bl                                                          
      Id State    Pos                                       
       1 enabled  34:5                                      
```

在这里，我们将禁用使用条目 (en) 事件**sxd**脚本调试器命令。 

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >sxd en                                                                              
sxd en                                                                                                                 
Event filter 'en' is now inactive                                                                                      
```

然后只需转，并让持续到最后的脚本。

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

再次执行的脚本方法，并观察被命中的断点。

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

此时，我们想要停止调试此脚本中，因此我们从其分离。  

```dbgcmd
>>> Debug [DebuggableSample 34:5] >.detach                  
.detach                                                     
Debugger has been detached from script!                     
```

然后键入 q 以退出。

```dbgcmd                             
q                                                           
This is a fun test                                          
Of the script debugger                                      
foo.a = 99                                                  
Caught and returned!                                        
Test                                                        
```

再次执行该函数将无法再中断到调试器。

```dbgcmd
0:007> dx @$scriptContents.outermost()
inside outer!
This is a fun test
Of the script debugger
foo.a = 99
Caught and returned!
Test
```

## <a name="span-idvscodespanspan-idvscodespanspan-idvscodespanjavascript-in-vscode---adding-intellisense"></a><span id="Vscode"></span><span id="vscode"></span><span id="VSCODE"></span>VSCode-添加 IntelliSense 中的 JavaScript

如果你想要使用调试器数据模型对象在 VSCode 中，可以使用 Windows 开发工具包中提供的定义文件。 IntelliSense 定义文件提供了所有 host.* 调试器对象 Api 的支持。 如果在 64 位电脑上的默认目录中安装该工具包，该文件夹位于：

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext\JsProvider.d.ts`

若要使用在 VSCode 中的 IntelliSense 定义文件：

1. 查找定义文件-JSProvider.d.ts

2. 将定义文件复制到您的脚本所在的文件夹。

3. 添加`/// <reference path="JSProvider.d.ts" />`到你的 JavaScript 脚本文件的顶部。

与你的 JavaScript 文件中该引用，VS Code 将自动为您提供 IntelliSense 主机除了在脚本中的结构提供的 JSProvider Api。 例如，键入"托管"。 你将看到所有可用的调试程序模型 Api 的 IntelliSense。


## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspanjavascript-resources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>JavaScript 资源


以下是可能会很有用，因为开发 JavaScript 调试扩展的 JavaScript 资源。

-   [编写 JavaScript 代码](https://msdn.microsoft.com/library/cte3c772.aspx)

-   [JScript 语言教程](https://msdn.microsoft.com/library/t895bwkh.aspx)

-   [Mozilla JavaScript 参考](https://developer.mozilla.org/docs/Web/JavaScript)

-   [WinJS：Windows JavaScript 库](https://developer.microsoft.com/windows/develop/winjs)

-   [ECMAScript 6-新功能：概述和比较](https://es6-features.org/)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[JavaScript 调试器的示例脚本](javascript-debugger-example-scripts.md)

[JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)











---
title: .scriptdebug (调试 JavaScript)
description: 使用.scriptdebug 命令来调试 JavaScript 的脚本。
keywords:
- .scriptdebug 调试 JavaScript Windows 调试
ms.date: 12/28/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .scriptdebug (Debug JavaScript)
api_type:
- NA
ms.openlocfilehash: cd1dd7119b2eca9716e7b4779319c37b538e62cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524888"
---
# <a name="scriptdebug-debug-javascript"></a>.scriptdebug (调试 JavaScript)

使用 **.scriptdebug**命令来调试 JavaScript 的脚本。

```dbgcmd
.scriptdebug FileName
```

### <a name="parameters"></a>参数

*FileName*

指定调试器 JavaScript 脚本进行调试的名称。

### <a name="span-idenvironmentspanenvironment"></a><span id="Environment"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>



## <a name="span-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span>其他信息

JavaScript 调试的概述，请参阅[JavaScript 调试器脚本-JavaScript 调试](javascript-debugger-scripting.md#DEBUGGING)。

>[!NOTE] 
> 若要使用 JavaScript 调试 WinDbg 预览，请以管理员身份运行调试器。
>


<a name="remarks"></a>备注
-------

在你之前调试 JavaScript 完成以下步骤。

1. 加载 JavaScript 脚本编写提供程序使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令。 

    ```dbgcmd
    0:000> .load jsprovider.dll
    ```

2. 加载示例脚本。

    ```dbgcmd
    0:000> .scriptload C:\MyScripts\DebuggableSample.js
    ```

若要开始主动进行调试脚本使用 **.scriptdebug**命令。

```dbgcmd
0:000> .scriptdebug C:\MyScripts\DebuggableSample.js
>>> ****** DEBUGGER ENTRY DebuggableSample ******
           No active debug event!

>>> Debug [DebuggableSample <No Position>] >
```

一旦你会看到提示 *>>> 调试 [DebuggableSample <No Position>] >* 和输入的请求，则位于脚本调试器。  

使用 **.help 获取**命令或 **？** 若要在 JavaScript 调试环境中显示的命令的列表。

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


### <a name="events"></a>事件

使用**sx**脚本调试器命令以查看可捕获的事件的列表。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sx              
sx                                                          
    ab  [   inactive] .... Break on script abort            
    eh  [   inactive] .... Break on any thrown exception    
    en  [   inactive] .... Break on entry to the script     
    uh  [     active] .... Break on unhandled exception     
```

使用**sxe**脚本调试器命令以启用任何中断行为。 若要开启条目时中断，以便该脚本将捕获到脚本调试器就立即执行其中的任何代码示例，使用此命令。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sxe en          
sxe en                                                      
Event filter 'en' is now active                             
```

使用**sxd**脚本调试器命令以禁用所有断点行为。

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >sxd en                                                                              
sxd en                                                                                                                 
Event filter 'en' is now inactive                                                                                      
```

### <a name="stack-trace"></a>堆栈跟踪

使用**k**命令以显示堆栈跟踪。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

### <a name="enumerating-variables"></a>枚举变量

使用 **??** 若要枚举的 JavaScript 变量的值。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >??someObj                
??someObj                                                   
someObj          : {...}                                    
    __proto__        : {...}                                
    a                : 0x63                                 
    b                : {...}                                
```


### <a name="breakpoints"></a>断点

使用以下断点命令来处理其他断点。


|           |                                |
|-----------|--------------------------------|
| bp <bpid> |        设置断点        |
| bd <bpid> |     禁用断点     |
| be <bpid> |     启用的断点      |
| bc <bpid> |      清除断点      |
|    bpc    | 当前行上设置断点 |
|    bl     |     列出断点     |

### <a name="flow-control---navigation"></a>流控制的导航

使用以下命令以在脚本中向前移动。

|   |                           |
|---|---------------------------|
|p  | 逐过程执行                 |
|的 VPN 连接下  | 中的步骤                   |
|g  | 继续脚本           |
|gu | 跳出                  |



### <a name="frames"></a>帧

使用以下命令以使用帧。


|                |                                |
|----------------|--------------------------------|
| .frame <index> | 切换到帧数 <index> |
|      .f+       |   切换到下一步堆栈帧   |
|      .f+       | 切换到上一个堆栈帧 |

### <a name="quiting"></a>Quiting

使用 **.detach**命令以 JavaScript 调试器分离。 

```dbgcmd
>>> Debug [DebuggableSample 34:5] >.detach                  
.detach                                                     
Debugger has been detached from script!                     
```

使用**q**命令退出 JavaScript 调试器。 

```dbgcmd
>>> Debug [<NONE> ] >q                                      
q                                                           
```


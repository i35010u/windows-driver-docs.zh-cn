---
title: .scriptdebug（调试 JavaScript）
description: 使用 scriptdebug 命令调试 JavaScript 脚本。
keywords:
- 。 scriptdebug 调试 JavaScript Windows 调试
ms.date: 02/02/2021
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .scriptdebug (Debug JavaScript)
api_type:
- NA
ms.openlocfilehash: 8006e3c5175e0cd88e6fa47d0bf554fbd062f28c
ms.sourcegitcommit: 5a7c96139b0ae0dd0d6aae6561f25e0b26a2c5b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2021
ms.locfileid: "99568861"
---
# <a name="scriptdebug-debug-javascript"></a>.scriptdebug（调试 JavaScript）

使用 **scriptdebug** 命令调试 JavaScript 脚本。

```dbgcmd
.scriptdebug FileName
```

### <a name="parameters"></a>参数

*FileName*

指定要调试的调试器 JavaScript 脚本的名称。

### <a name="span-idenvironmentspanenvironment"></a><span id="Environment"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>



## <a name="span-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span>附加信息

有关 JavaScript 调试的概述，请参阅  [Javascript 调试器脚本-Javascript 调试](javascript-debugger-scripting.md#DEBUGGING)。

>[!NOTE] 
> 若要对 WinDbg Preview 使用 JavaScript 调试，请以管理员身份运行调试器。
>


<a name="remarks"></a>备注
-------

在调试 JavaScript 之前，请完成以下步骤。

1. 加载示例脚本。

    ```dbgcmd
    0:000> .scriptload C:\MyScripts\DebuggableSample.js
    ```

若要开始主动调试脚本，请使用 **scriptdebug** 命令。

```dbgcmd
0:000> .scriptdebug C:\MyScripts\DebuggableSample.js
>>> ****** DEBUGGER ENTRY DebuggableSample ******
           No active debug event!

>>> Debug [DebuggableSample <No Position>] >
```

看到提示符 *>>> 调试 [DebuggableSample <No Position> ] >* 和输入请求时，就会出现在脚本调试器内。  

使用 " **help** " 命令或 **？** 显示 JavaScript 调试环境中的命令列表。

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

使用 **sx** 脚本调试器命令可以查看可以捕获的事件列表。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sx              
sx                                                          
    ab  [   inactive] .... Break on script abort            
    eh  [   inactive] .... Break on any thrown exception    
    en  [   inactive] .... Break on entry to the script     
    uh  [     active] .... Break on unhandled exception     
```

使用 **sxe** script 调试器命令启用任何中断行为。 例如，若要在输入时启用中断，以便在脚本调试器中的任何代码执行时，脚本将捕获到脚本调试器中，请使用此命令。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sxe en          
sxe en                                                      
Event filter 'en' is now active                             
```

使用 **sxd** script 调试器命令可以禁用任何断点行为。

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >sxd en                                                                              
sxd en                                                                                                                 
Event filter 'en' is now inactive                                                                                      
```

### <a name="stack-trace"></a>堆栈跟踪

使用 **k** 命令显示堆栈跟踪。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

### <a name="enumerating-variables"></a>枚举变量

使用 **？？** 枚举 JavaScript 变量的值。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >??someObj                
??someObj                                                   
someObj          : {...}                                    
    __proto__        : {...}                                
    a                : 0x63                                 
    b                : {...}                                
```


### <a name="breakpoints"></a>断点

使用以下断点命令处理其他断点。


**bp <bpid>**：设置断点

**bd <bpid>**：禁用断点

**为 <bpid>**：启用断点

**bc <bpid>**：清除断点

**bpc**：在当前行上设置断点

**bl**：列出断点 () 


### <a name="flow-control---navigation"></a>流控制-导航

使用以下命令在脚本中向前移动。

**p**：逐过程

**t**：单步执行

**g**：继续编写脚本

**gu**：跳出




### <a name="frames"></a>文本框

使用以下命令来处理框架。


**。 frame <index>**：切换到帧号<index>

**。 f +**：切换到下一个堆栈帧

**。 f +**：切换到上一个堆栈帧


### <a name="quiting"></a>Quiting

使用 **detach** 命令分离 JavaScript 调试器。 

```dbgcmd
>>> Debug [DebuggableSample 34:5] >.detach                  
.detach                                                     
Debugger has been detached from script!                     
```

使用 **q** 命令退出 JavaScript 调试器。 

```dbgcmd
>>> Debug [<NONE> ] >q                                      
q                                                           
```


---
title: 时光穿越调试 - JavaScript 自动化
description: 本部分介绍如何使用 JavaScript 自动化来处理 TTD 跟踪。
ms.date: 09/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: ab21be9eb2ab670a51b95c1813a93f46bb6d4b18
ms.sourcegitcommit: ee3e2259aafc844cc43cce62299a72649cf89212
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91353610"
---
# <a name="time-travel-debugging---javascript-automation"></a>时光穿越调试 - JavaScript 自动化

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png)

可以通过多种方式（例如命令自动化或使用查询从跟踪文件中查找事件数据）使用 JavaScript 自动化来处理 TTD 跟踪。

有关使用 JavaScript 的常规信息，请参阅 [Javascript 调试器脚本](javascript-debugger-scripting.md)。 还有 [JavaScript 调试器示例脚本](javascript-debugger-example-scripts.md)。

## <a name="javascript-ttd-command-automation"></a>JavaScript TTD 命令自动化

使用 JavaScript 实现 TTD 自动化的一种方法是发送命令以自动处理时间旅行跟踪文件。

### <a name="moving-in-a-trace-file"></a>在跟踪文件中移动

此 JavaScript 演示如何使用 [！！](time-travel-debugging-extension-tt.md) 命令移到开始时间跟踪。

```javascript
var dbgControl = host.namespace.Debugger.Utility.Control;  
dbgControl.ExecuteCommand("!tt 0",false);
host.diagnostics.debugLog(">>> Sent command to move to the start of the TTD file \n");
```

我们可以将此函数设置为 ResetTrace 函数，并在 WinDbg Preview 中使用 JavaScript UI 将其另存为 ResetTrace.js。

```javascript
// WinDbg TTD JavaScript ResetTraceCmd Sample

"use strict";

function ResetTraceCmd()
{
    var dbgControl = host.namespace.Debugger.Utility.Control;  
    dbgControl.ExecuteCommand("!tt 0",false);
    host.diagnostics.debugLog(">>> Sent command to move to the start of the TTD file \n");
}
```

在 WinDbg Preview 中加载 TTD 文件后，请在调试器命令窗口中使用 dx 命令调用函数 ResetTraceCmd ( # A1 函数。

```dbgcmd
0:000> dx Debugger.State.Scripts.ResetTrace.Contents.ResetTraceCmd()
>>> Sent command to move to the start of the TTD file
Debugger.State.Scripts.ResetTrace.Contents.ResetTrace()
```

## <a name="limitations-of-sending-commands"></a>发送命令的限制

但除最简单的情况外，发送命令的方法也存在缺点。 它依赖于文本输出。 而且，分析输出会导致代码脆弱且难以维护。 更好的方法是直接使用 TTD 对象。

下面的示例演示如何直接使用对象直接完成同一任务。

```javascript
// WinDbg TTD JavaScript ResetTrace Sample

"use strict";

function ResetTrace()
{
    host.currentProcess.TTD.SetPosition(0);
    host.diagnostics.debugLog(">>> Set position to the start of the TTD file \n");
}

```

运行此代码后，可以移动到跟踪文件的开头。

```dbgcmd
0:000> dx Debugger.State.Scripts.ResetTrace.Contents.ResetTrace()
(948.148c): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: F:0
>>> Set position to the start of the TTD file
```

在此示例中，ResetTraceEnd 函数将位置设置为跟踪末尾，并使用 [Thread.currentthread.priority](time-travel-debugging-thread-objects.md) 位置对象显示当前和新位置。

```javascript

// WinDbg TTD JavaScript Sample to Reset Trace using objects directly
// and display current and new position

function ResetTraceEnd()
{
   var PositionOutputStart = host.currentThread.TTD.Position;
   host.diagnostics.debugLog(">>> Current position in trace file:  "+ PositionOutputStart +"\n");
   host.currentProcess.TTD.SetPosition(100);
   var PositionOutputNew = host.currentThread.TTD.Position;
   host.diagnostics.debugLog(">>> New position in trace file:  "+ PositionOutputNew +"\n");
}
```

运行此代码将显示当前和新的位置。


```dbgcmd
0:000> dx Debugger.State.Scripts.ResetTrace.Contents.ResetTraceEnd()
>>> Current position in trace file:  F:0
(948.148c): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: D3:1
>>> New position in trace file:  D3:1
```

在此展开的示例中，比较起始位置和结束位置值，以确定跟踪中的位置是否发生了更改。

```javascript
// WinDbg TTD JavaScript ResetTraceEx Sample

"use strict";

function ResetTraceEx()
{
    const PositionOutputStart = host.currentThread.TTD.Position;
    host.diagnostics.debugLog(">>> Current position in trace file:  "+ PositionOutputStart +"\n");
  
    host.currentProcess.TTD.SetPosition(0);

    const PositionOutputNew = host.currentThread.TTD.Position;
    host.diagnostics.debugLog(">>> New position in trace file:  "+ PositionOutputNew +"\n");

    if (parseInt(PositionOutputStart,16) != parseInt(PositionOutputNew,16))
    {
        host.diagnostics.debugLog(">>> Set position to the start of the TTD file  \n");
    }
    else
    {
        host.diagnostics.debugLog(">>> Position was already set to the start of the TTD file \n");
    }
}

```

在此示例中，将显示一条消息，表明我们已在跟踪文件开始处准备就绪。

```dbgcmd
0:000> dx Debugger.State.Scripts.ResetTrace.Contents.ResetTraceEx()
>>> Current position in trace file:  F:0
(948.148c): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: F:0
>>> New position in trace file:  F:0
>>> Position was already set to the start of the TTD file
```

若要测试该脚本，请使用 [！！](time-travel-debugging-extension-tt.md) 命令在跟踪文件中导航到一半。

```dbgcmd
0:000> !tt 50
Setting position to 50% into the trace
Setting position: 71:0
```

运行该脚本后，将显示适当的消息，指示该位置设置为 TTD 跟踪的开头。

```dbgcmd
0:000> dx Debugger.State.Scripts.ResetTrace.Contents.ResetTraceEx()
>>> Current position in trace file:  71:0
(948.148c): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: F:0
>>> New position in trace file:  F:0
>>> Set position to the start of the TTD file  
```

## <a name="indexing-a-time-travel-trace-file"></a>为时间段编制索引旅行跟踪文件

如果只将跟踪文件复制到另一台计算机上，则需要对其重新编制索引。 有关详细信息，请参阅 [行程调试-使用跟踪文件](time-travel-debugging-trace-file-information.md)。

此代码显示了一个示例 IndexTrace 函数，该函数显示重新为跟踪文件编制索引需要多长时间。

```javascript
function IndexTrace()
{
    var timeS = (new Date()).getTime();
    var output = host.currentProcess.TTD.Index.ForceBuildIndex();
    var timeE = (new Date()).getTime();
    host.diagnostics.debugLog("\n>>> Trace was indexed in " + (timeE - timeS) + " ms\n");
}

```

下面是小跟踪文件的输出。

```dbgcmd
0:000> dx Debugger.State.Scripts.TTDUtils.Contents.IndexTrace()

>>> Trace was indexed in 2 ms
```

### <a name="adding-a-try-catch-statement"></a>添加 try catch 语句

若要查看在运行索引时是否引发了错误，请在 try catch 语句中包含索引代码。

```javascript

function IndexTraceTry()
{
    var timeS = (new Date()).getTime();
    try
    {
         var IndexOutput =  host.currentProcess.TTD.Index.ForceBuildIndex();
         host.diagnostics.debugLog("\n>>> Index Return Value: " + IndexOutput + "\n");
         var timeE = (new Date()).getTime();
         host.diagnostics.debugLog("\n>>> Trace was successfully indexed in " + (timeE - timeS) + " ms\n");
     }

    catch(err)
    {
         host.diagnostics.debugLog("\n>>> Index Failed! \n");
         host.diagnostics.debugLog("\n>>> Index Return Value: " + IndexOutput + "\n");
         host.diagnostics.debugLog("\n>>> Returned error: " + err.name + "\n");
    }
}

```

如果索引成功，则会显示脚本输出。

```dbgcmd
0:000> dx Debugger.State.Scripts.TTDUtils.Contents.IndexTraceTry()

>>> Index Return Value: Loaded

>>> Trace was successfully indexed in 1 ms
```

如果无法为跟踪编制索引（例如，在调试器中未加载跟踪），则运行 catch 循环代码。

```dbgcmd
0:007> dx Debugger.State.Scripts.TTDUtils.Contents.IndexTraceTry()

>>> Index Failed!

>>> Index Return Value: undefined

>>> Returned error: TypeError
```

## <a name="javascript-ttd-objects-queries"></a>JavaScript TTD 对象查询

JavaScript 和 TTD 的更高级用法是查询旅行对象查找跟踪中已发生的特定调用或事件。 有关 TTD 对象的详细信息，请参阅：

[行程调试对象简介](time-travel-debugging-object-model.md)

[JavaScript 扩展中的本机调试器对象 - 调试器对象详细信息](native-objects-in-javascript-extensions-debugger-objects.md)

[Dx](dx--display-visualizer-variables-.md)命令显示调试器数据模型中的信息，并使用 LINQ 语法支持查询。 Dx 对于实时查询对象非常有用。 这样，就可以使用 JavaScript 自动构建所需查询的原型。 Dx 命令提供 tab 自动补全，这在浏览对象模型时非常有用。 有关使用 LINQ 查询和调试器对象的常规信息，请参阅 [将 Linq 与调试器对象配合使用](using-linq-with-the-debugger-objects.md)。

此 dx 命令对某个 API 的所有调用进行计数，在此示例中为 *GetLastError*。

```dbgcmd
0:000> dx @$cursession.TTD.Calls("kernelbase!GetLastError").Count()

@$cursession.TTD.Calls("kernelbase! GetLastError").Count() : 0x12
```

此命令在整个旅行跟踪中查找调用 GetLastError 的时间。

```dbgcmd
0:000> dx @$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0)

@$cursession.TTD.Calls("kernelbase!GetLastError").Where(c => c.ReturnValue != 0)
    [0x0]
    [0x1]
    [0x2]
    [0x3]
```

### <a name="string-comparisons-for-ttdcalls-object-to-locate-calls"></a>TTD 的字符串比较。调用对象以定位调用

此示例命令演示了如何使用字符串比较来查找特定的调用。 在此示例中，查询在[CreateFileW 函数](/windows/win32/api/fileapi/nf-fileapi-createfilew)的*lpFileName*参数中查找字符串 "OLE"。

```dbgcmd
dx -r2 @$cursession.TTD.Calls("kernelbase!CreateFileW").Where(x => x.Parameters.lpFileName.ToDisplayString("su").Contains("OLE"))
```

添加。Select 语句来打印 Timestart 和 *lpFileName* 参数的值。

```dbgcmd
dx -r2 @$cursession.TTD.Calls("kernelbase!CreateFileW").Where(x => x.Parameters.lpFileName.ToDisplayString("su").Contains("OLE")).Select(x => new { TimeStart = x.TimeStart, lpFileName = x.Parameters.lpFileName })
```

如果 TTD，则会生成此输出 [。](time-travel-debugging-calls-objects.md) 找到包含目标信息的调用对象。

```dbgcmd
    [0x0]
        TimeStart        : 6E37:590
        lpFileName       : 0x346a78be90 : "C:\WINDOWS\SYSTEM32\OLEACCRC.DLL" [Type: wchar_t *]
```

## <a name="displaying-the-number-of-calls-in-a-trace"></a>显示跟踪中的调用数

使用 dx 命令浏览要使用的对象后，可以自动将其与 JavaScript 一起使用。 在这个简单的示例中， [TTD。调用](time-travel-debugging-calls-objects.md) 对象用于对 kernelbase 的调用进行计数 *！GetLastError*。

```javascript
function CountLastErrorCalls()
{
    var LastErrorCalls = host.currentSession.TTD.Calls("kernelbase!GetLastError");
    host.diagnostics.debugLog(">>> GetLastError calls in this TTD recording: " +  LastErrorCalls.Count() +" \n");
}
```

将该脚本保存在 TTDUtils.js 文件中，并使用 dx 命令调用该脚本以显示 kernelbase 数的计数！GetLastError 在跟踪文件中。

```dbgcmd

0:000> dx Debugger.State.Scripts.TTDUtils.Contents.CountLastErrorCalls()
>>> GetLastError calls in this TTD recording: 18
```

## <a name="displaying-the-frames-in-a-stack"></a>显示堆栈中的帧

若要显示堆栈中的帧，请使用数组。

```javascript
function DisplayStack()
{
// Create an array of stack frames in the current thread
const Frames = Array.from(host.currentThread.Stack.Frames);
host.diagnostics.debugLog(">>> Printing stack \n");
// Print out all of the frame entries in the array
for(const [Idx, Frame] of Frames.entries())
    {
        host.diagnostics.debugLog(">>> Stack Entry -> " + Idx + ":  "+ Frame + " \n");
    }
}
```

在此示例跟踪中，将显示一个堆栈条目。

```dbgcmd
0:000> dx Debugger.State.Scripts.TTDUtils.Contents.DisplayStack()
>>> Printing stack
>>> Stack Entry -> 0:  ntdll!LdrInitializeThunk + 0x21
```

## <a name="locating-an-event-and-displaying-the-stack"></a>定位事件并显示堆栈

在此代码中，所有异常事件都位于，并使用循环来移动到每个事件。 然后， [TTD 线程对象](time-travel-debugging-thread-objects.md) 的 currentThread.ID 用于显示线程 ID，而 thread.currentthread.priority 用于显示堆栈中的所有帧。

```javascript

function HardwareExceptionDisplayStack()
{
var exceptionEvents = host.currentProcess.TTD.Events.Where(t => t.Type == "Exception");
    for (var curEvent of exceptionEvents)
    {
        // Move to the current event position
        curEvent.Position.SeekTo();
        host.diagnostics.debugLog(">>> The Thread ID (TID) is : " + host.currentThread.Id + "\n");
        // Create an array of stack frames in the current thread
        const Frames = Array.from(host.currentThread.Stack.Frames);
        host.diagnostics.debugLog(">>> Printing stack \n");
        // Print out all of the frame entries in the array
        for(const [Idx, Frame] of Frames.entries()) {
            host.diagnostics.debugLog(">>> Stack Entry -> " + Idx + ":  "+ Frame + " \n");
        }
    host.diagnostics.debugLog("\n");
    }
}
```

输出显示异常事件、TID 和堆栈帧的位置。  

```dbgcmd
0:000> dx Debugger.State.Scripts.TTDUtils.Contents.HardwareExceptionDisplayStack()
(948.148c): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 91:0
>>> The Thread ID (TID) is : 5260
>>> Printing stack
>>> Stack Entry -> 0:  0x540020
>>> Stack Entry -> 1:  0x4d0049
>>> Stack Entry -> 2:  DisplayGreeting!__CheckForDebuggerJustMyCode + 0x16d
>>> Stack Entry -> 3:  DisplayGreeting!mainCRTStartup + 0x8
>>> Stack Entry -> 4:  KERNEL32!BaseThreadInitThunk + 0x19
>>> Stack Entry -> 5:  ntdll!__RtlUserThreadStart + 0x2f
>>> Stack Entry -> 6:  ntdll!_RtlUserThreadStart + 0x1b

```

## <a name="locating-an-event-and-sending-two-commands"></a>查找事件并发送两个命令

查询 TTD 对象和发送命令可以根据需要进行组合。 此示例在 ThreadCreated 类型的 TTD 跟踪中查找每个事件，移动到该位置，并发送 [~ 线程状态](---thread-status-.md) 和 [！失控](-runaway.md) 命令以显示线程状态。

```javascript
function ThreadCreateThreadStatus()
{
var threadEvents = host.currentProcess.TTD.Events.Where(t => t.Type == "ThreadCreated");
    for (var curEvent of threadEvents)
    {
        // Move to the current event position
       curEvent.Position.SeekTo();
        // Display Information about threads
       host.namespace.Debugger.Utility.Control.ExecuteCommand("~", false);
       host.namespace.Debugger.Utility.Control.ExecuteCommand("!runaway 7", false);
    }
}
```

运行代码将在发生异常的时间显示线程状态。

```dbgcmd
0:000> dx Debugger.State.Scripts.TTDUtils.Contents.ThreadCreateThreadStatus()
(948.148c): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: F:0
.  0  Id: 948.148c Suspend: 4096 Teb: 00a33000 Unfrozen
User Mode Time
  Thread       Time
    0:148c     0 days 0:00:00.000
Kernel Mode Time
  Thread       Time
    0:148c     0 days 0:00:00.000
Elapsed Time
  Thread       Time
    0:148c     3474 days 2:27:43.000
```

## <a name="chaining-utility-functions-together"></a>将实用工具函数结合在一起

在此最后的示例中，我们可以调用之前创建的实用工具函数。 首先，我们使用 *IndexTraceTry* 为跟踪编制索引，然后调用 *ThreadCreateThreadStatus*。 然后，使用 *ResetTrace* 移动到跟踪的开头，最后调用 *HardwareExceptionDisplayStack*。

```JavaScript
function ProcessTTDFiles()
{
    try
    {
    IndexTraceTry()
    ThreadCreateThreadStatus()
    ResetTrace()
    HardwareExceptionDisplayStack()
    }

    catch(err)
    {
         host.diagnostics.debugLog("\n >>> Processing of TTD file failed \n");
    }

}
```

在包含硬件例外的跟踪文件上运行此脚本会生成此输出。

```dbgcmd
0:000> dx Debugger.State.Scripts.TTDUtils.Contents.ProcessTTDFiles()

>>> Index Return Value: Loaded

>>> Trace was successfully indexed in 0 ms
(948.148c): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: F:0
.  0  Id: 948.148c Suspend: 4096 Teb: 00a33000 Unfrozen
User Mode Time
  Thread       Time
    0:148c     0 days 0:00:00.000
Kernel Mode Time
  Thread       Time
    0:148c     0 days 0:00:00.000
Elapsed Time
  Thread       Time
    0:148c     3474 days 2:27:43.000
>>> Printing stack
>>> Stack Entry -> 0:  ntdll!LdrInitializeThunk
>>> Current position in trace file:  F:0
(948.148c): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: F:0
>>> New position in trace file:  F:0
(948.148c): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 91:0
>>> The Thread ID (TID) is : 5260
>>> Printing stack
>>> Stack Entry -> 0:  0x540020
>>> Stack Entry -> 1:  0x4d0049
>>> Stack Entry -> 2:  DisplayGreeting!__CheckForDebuggerJustMyCode + 0x16d
>>> Stack Entry -> 3:  DisplayGreeting!mainCRTStartup + 0x8
>>> Stack Entry -> 4:  KERNEL32!BaseThreadInitThunk + 0x19
>>> Stack Entry -> 5:  ntdll!__RtlUserThreadStart + 0x2f
>>> Stack Entry -> 6:  ntdll!_RtlUserThreadStart + 0x1b

```

---

## <a name="see-also"></a>另请参阅

[时光穿越调试 - 概述](time-travel-debugging-overview.md)

[行程调试对象简介](time-travel-debugging-object-model.md)

[JavaScript 扩展中的本机调试器对象 - 调试器对象详细信息](native-objects-in-javascript-extensions-debugger-objects.md)

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[JavaScript 调试器示例脚本](javascript-debugger-example-scripts.md)
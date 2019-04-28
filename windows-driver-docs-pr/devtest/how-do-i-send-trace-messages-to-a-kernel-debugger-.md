---
title: 如何将跟踪消息发送到内核调试程序
description: 如何将跟踪消息发送到内核调试程序
ms.assetid: 867791a7-30a5-4539-be85-61f1716c279a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2783a065d9dce8080d559cefb394c47c5d29d483
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347719"
---
# <a name="how-do-i-send-trace-messages-to-a-kernel-debugger"></a>如何将跟踪消息发送到内核调试器？


几种方法可用于将跟踪消息重定向到内核模式调试程序。 讨论几个。

可以重定向跟踪消息，KD 到或的 Windbg 中，附加者为准。 必须附加调试器，通过 COM 端口与调试 （调制解调器） 电缆或通过使用 IEEE 1394 电缆的 1394年 （"火线"） 端口。 不能将跟踪消息重定向到其他内核调试程序，如 NTSD。

若要在调试器中显示跟踪消息，wmitrace.dll 和 traceprt.dll 必须在主计算机上的调试程序的搜索路径中。 中包含这些 Dll[有关 Windows 调试工具](https://go.microsoft.com/fwlink/p/?linkid=8708)此外，若要使调试器能够找到[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)跟踪消息，TMF 文件必须包含在调试器的搜索在主计算机上的路径。 若要设置的调试程序的搜索路径，请使用 ！ wmitrace.searchpath 专用调试器扩展，或设置的值 %跟踪\_格式\_搜索\_PATH %环境变量。

有关详细信息，搜索 **！ wmitrace**中*对于 Windows 调试工具*。

### <a name="span-idlogmanspanspan-idlogmanspanlogman"></a><span id="logman"></span><span id="LOGMAN"></span>Logman

使用以下 Logman 命令将跟踪消息重定向到内核模式调试程序：

```
logman start TraceSession -ets -mode KernelFilter -bs 3
```

**-Ets**参数启动不受性能日志和警报服务的事件跟踪会话。 **-模式**参数将激活高级的选项，包括**KernelFilter**选项。

**-Bs**参数设置为 3 KB，调试程序的最大缓冲区大小跟踪会话缓冲区大小。 如果省略此参数时，调试器会话将无法正常运行。

Logman 包含在 Windows XP 和更高版本的 Windows。

### <a name="span-idtracelogspanspan-idtracelogspantracelog"></a><span id="tracelog"></span><span id="TRACELOG"></span>跟踪日志

使用以下[Tracelog](tracelog.md)命令重定向到内核模式调试程序的跟踪消息：

```
tracelog -start MyTrace -guid MyProvider.ctl -rt -kd
```

**Guid**参数指定[跟踪提供程序](trace-provider.md)。 **-Rt**参数指定的实时跟踪会话。 **-Kd**参数将跟踪消息重定向到内核调试程序并设置最大缓冲区大小为 3KB，调试程序的最大值。

有关示例，请参阅[示例 16:在调试器中查看跟踪消息](example-16--viewing-trace-messages-in-a-debugger.md)。

跟踪日志工具位于\\跟踪\\*&lt;平台&gt;* 子目录 WDK，其中*&lt;平台&gt;* 是 i386、 amd64 或 ia64。

### <a name="span-idtraceviewspanspan-idtraceviewspantraceview"></a><span id="traceview"></span><span id="TRACEVIEW"></span>TraceView

[TraceView](traceview.md)具有图形用户界面。

可以将跟踪消息重定向到内核调试程序，创建跟踪会话时。 上**日志会话选项**页上，单击**高级日志会话选项**，单击**日志会话参数选项**选项卡，然后更改的值**Windbg**选项设置为 **，则返回 TRUE**。 运行跟踪会话时，不能更改此选项。

工具中位于 TraceView\\跟踪\\*&lt;平台&gt;* 子目录 WDK，其中*&lt;平台&gt;* 是 i386、 amd64 或 ia64。

 

 






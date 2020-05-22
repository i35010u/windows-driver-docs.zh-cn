---
title: 如何实现将跟踪消息发送到内核调试器
description: 如何实现将跟踪消息发送到内核调试器
ms.assetid: 867791a7-30a5-4539-be85-61f1716c279a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 956f11355ab3a1cfee8484a0f06680ee5b91d91d
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769619"
---
# <a name="how-do-i-send-trace-messages-to-a-kernel-debugger"></a>如何将跟踪消息发送到内核调试器？


您可以使用多种方法将跟踪消息重定向到内核模式调试器。 这里讨论了一些内容。

可以将跟踪消息重定向到 KD，或重定向到 Windbg，无论附加哪个。 必须通过带有调试（零调制解调器）电缆的 COM 端口或通过使用 IEEE 1394 电缆的1394（"火线"）端口来附加调试器。 不能将跟踪消息重定向到其他内核调试器，如 NTSD。

若要在调试器中显示跟踪消息，wmitrace 和 traceprt 必须在主计算机上的调试器搜索路径中。 这些 Dll 也包含在[Windows 调试工具](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)中，若要使调试器能够查找跟踪消息的[跟踪消息格式（tmf）文件](trace-message-format-file.md)，则 tmf 文件必须在主计算机上的调试器搜索路径中。 若要设置调试器的搜索路径，请使用！ searchpath 专用调试程序扩展或设置% 跟踪 \_ 格式 \_ 搜索 \_ 路径% 环境变量的值。

有关详细信息，请在*Windows 调试工具*中搜索 **！ wmitrace** 。

### <a name="span-idlogmanspanspan-idlogmanspanlogman"></a><span id="logman"></span><span id="LOGMAN"></span>Logman

使用以下 Logman 命令将跟踪消息重定向到内核模式调试器：

```
logman start TraceSession -ets -mode KernelFilter -bs 3
```

**-Ets**参数启动不受性能日志和警报服务控制的事件跟踪会话。 **-Mode**参数激活高级选项，包括**KernelFilter**选项。

**-Bs.1770**参数将跟踪会话的缓冲区大小设置为 3 KB，即调试器的最大缓冲区大小。 如果省略此参数，则调试器会话将无法正常运行。

Logman 包含在 Windows XP 和更高版本的 Windows 中。

### <a name="span-idtracelogspanspan-idtracelogspantracelog"></a><span id="tracelog"></span><span id="TRACELOG"></span>Tracelog

使用以下[Tracelog](tracelog.md)命令将跟踪消息重定向到内核模式调试器：

```
tracelog -start MyTrace -guid MyProvider.ctl -rt -kd
```

**-Guid**参数指定[跟踪提供程序](trace-provider.md)。 **-Rt**参数指定实时跟踪会话。 **-Kd**参数将跟踪消息重定向到内核调试器，并将最大缓冲区大小设置为 3 KB，最大值为调试器。

有关示例，请参阅[示例16：在调试器中查看跟踪消息](example-16--viewing-trace-messages-in-a-debugger.md)。

Tracelog 位于 WDK 的 tools \\ 跟踪 \\ * &lt; &gt; 平台*子目录中，其中* &lt; &gt; Platform*为 i386、amd64 或 ia64。

### <a name="span-idtraceviewspanspan-idtraceviewspantraceview"></a><span id="traceview"></span><span id="TRACEVIEW"></span>TraceView

[TraceView](traceview.md)有一个图形用户界面。

创建跟踪会话时，可以将跟踪消息重定向到内核调试器。 在 "**日志会话选项**" 页面上，单击 "**高级日志会话选项**"，单击 "**日志会话参数选项**" 选项卡，然后将**Windbg**选项的值更改为 " **TRUE**"。 当跟踪会话正在运行时，不能更改此选项。

TraceView 位于 WDK 的 tools \\ 跟踪 \\ * &lt; &gt; 平台*子目录中，其中* &lt; &gt; Platform*为 i386、amd64 或 ia64。

 

 






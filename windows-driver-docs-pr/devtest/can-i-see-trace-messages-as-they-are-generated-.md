---
title: 生成可以查看跟踪消息
description: 生成可以查看跟踪消息
ms.assetid: 21d8606b-5693-4f50-81f9-c5c3a65c0550
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e60b1b65a224878517ef50ff70c9dddb7b316f4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545367"
---
# <a name="can-i-see-trace-messages-as-they-are-generated"></a>生成可以查看跟踪消息？


是。 若要查看的跟踪消息生成，使用中的实时跟踪会话选项[TraceView](traceview.md)， [Tracelog](tracelog.md)，或[Tracefmt](tracefmt.md)。 这些工具包括在工具\\跟踪\\&lt;*平台*&gt;子目录的 Microsoft Windows Driver Kit (WDK)，其中&lt; *平台*&gt;是 i386、 amd64 或 ia64。

[跟踪提供程序](trace-provider.md)而无需包含任何特殊代码，以支持实时跟踪。

### <a name="span-idtraceviewspanspan-idtraceviewspantraceview"></a><span id="traceview"></span><span id="TRACEVIEW"></span>TraceView

[TraceView](traceview.md)可以开始显示跟踪消息生成实时跟踪会话。 若要使用 TraceView 进行实时监视：

1.  启动 TraceView。

2.  上**文件**菜单上，单击**新建日志会话**。

3.  单击**添加提供程序**。

4.  选择**CTL (控制 GUID) 文件**选项。 然后单击省略号按钮 (**...**) 来查找[控制 GUID 文件](control-guid-file.md)提供程序。

5.  单击**选择 TMF 文件**。

6.  单击**外**，找到[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)提供程序，请单击**打开**，然后单击**完成**。

7.  单击“下一步” 。

8.  上**日志会话选项**页上，确认**实时显示**复选框处于选中状态 （已选中）。

    你可以选择其他选项以指定[跟踪标志](trace-flags.md)并[跟踪级别](trace-level.md)，或自定义跟踪会话。

9.  单击“完成” 。

有关详细信息，请在 TraceView 上,**帮助**菜单上，单击**帮助主题**。

### <a name="span-idtracelogspanspan-idtracelogspantracelog"></a><span id="tracelog"></span><span id="TRACELOG"></span>跟踪日志

跟踪日志可以启动、 停止和更新实时跟踪会话。

若要使用 Tracelog 启动实时跟踪会话，请使用 **-rt** （实时） 参数在启动跟踪会话的命令。

以下命令启动名为"My Trace"的提供程序具有一个跟踪会话 Guid MyProvider.ctl 中列出其控件[控制 GUID 文件](control-guid-file.md)。 **-Rt**参数指定的实时跟踪会话。

```
tracelog -start MyTrace -guid MyProvider.ctl -rt
```

有关详细示例，请参阅[示例 10:启动实时跟踪会话](example-10--starting-a-real-time-trace-session.md)。

若要查看来自实时跟踪会话的跟踪消息，请使用[Tracefmt](tracefmt.md)。

### <a name="span-idtracefmtspanspan-idtracefmtspantracefmt"></a><span id="tracefmt"></span><span id="TRACEFMT"></span>Tracefmt

[Tracefmt](tracefmt.md)可以显示从实时跟踪会话的跟踪消息。 在实时模式下，Tracefmt 格式化并写入到文件时显示的消息。

下面的命令显示来自"MyTrace"实时跟踪会话的跟踪消息。 **-Rt**参数指定的实时会话。 **-P**参数指示的路径[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)的跟踪消息。 **-显示**参数指示 Tracefmt 显示跟踪消息到达从缓冲区。 **-O**参数指定输出文件的位置。

```
tracefmt -rt MyTrace -p c:\tracing -display -o mytrace.txt
```

有关详细示例，请参阅[示例 5:格式设置实时跟踪会话](example-5--formatting-real-time-trace-sessions.md)。

 

 






---
title: 是否可以在生成跟踪消息时看到这些消息
description: 是否可以在生成跟踪消息时看到这些消息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d991fe7284371ff1532822184f7fe93686673bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791565"
---
# <a name="can-i-see-trace-messages-as-they-are-generated"></a>是否可以看到生成的跟踪消息？


是的。 若要在生成跟踪消息时查看这些消息，请使用 [TraceView](traceview.md)、 [Tracelog](tracelog.md)或 [Tracefmt](tracefmt.md)中的实时跟踪会话选项。 这些工具包含在 \\ \\ &lt; *Platform* &gt; Microsoft Windows 驱动程序工具包 (WDK) 的工具跟踪平台子目录中，其中 &lt; *Platform* &gt; 为 i386、amd64 或 ia64。

[跟踪提供程序](trace-provider.md) 不必包含任何特殊代码即可支持实时跟踪。

### <a name="span-idtraceviewspanspan-idtraceviewspantraceview"></a><span id="traceview"></span><span id="TRACEVIEW"></span>TraceView

[TraceView](traceview.md) 可以启动实时跟踪会话，它会在生成跟踪消息时显示这些消息。 使用 TraceView 进行实时监视：

1.  启动 TraceView。

2.  在 " **文件** " 菜单上，单击 " **创建新的日志会话**"。

3.  单击 **“添加提供程序”**。

4.  选择 **CTL (控件 GUID) 文件** "选项。 然后单击省略号按钮 " (**...** ") 查找提供程序的 [控件 GUID 文件](control-guid-file.md) 。

5.  单击 " **选择 TMF 文件**"。

6.  单击 " **添加**"，找到提供程序 [ () 文件的跟踪消息格式](trace-message-format-file.md) ，单击 " **打开**"，然后单击 " **完成**"。

7.  单击 **“下一步”** 。

8.  在 " **日志会话选项** " 页面上，验证是否选中了 " **实时显示** " 复选框 (选中) "。

    您可以选择其他选项来指定 [跟踪标志](trace-flags.md) 和 [跟踪级别](trace-level.md)，或自定义跟踪会话。

9.  单击“完成”。

有关详细信息，请在 TraceView 中的 " **帮助** " 菜单上，单击 " **帮助主题**"。

### <a name="span-idtracelogspanspan-idtracelogspantracelog"></a><span id="tracelog"></span><span id="TRACELOG"></span>Tracelog

Tracelog 可以启动、停止和更新实时跟踪会话。

若要使用 Tracelog 启动实时跟踪会话，请使用命令中的 **-rt** (实时) 参数启动跟踪会话。

下面的命令使用 MyProvider[控件 guid 文件](control-guid-file.md)中列出了控件 guid 的提供程序启动名为 "My trace" 的跟踪会话。 **-Rt** 参数指定实时跟踪会话。

```
tracelog -start MyTrace -guid MyProvider.ctl -rt
```

有关详细示例，请参阅 [示例10：启动 Real-Time 跟踪会话](example-10--starting-a-real-time-trace-session.md)。

若要查看实时跟踪会话中的跟踪消息，请使用 [Tracefmt](tracefmt.md)。

### <a name="span-idtracefmtspanspan-idtracefmtspantracefmt"></a><span id="tracefmt"></span><span id="TRACEFMT"></span>Tracefmt

[Tracefmt](tracefmt.md) 可以显示实时跟踪会话中的跟踪消息。 在实时模式下，Tracefmt 会在将消息写入到文件中时对其进行格式设置和显示。

以下命令显示 "MyTrace" 实时跟踪会话中的跟踪消息。 **-Rt** 参数指定实时会话。 **-P** 参数指示跟踪消息 [格式 () 文件](trace-message-format-file.md)的路径。 **-Display** 参数指示 Tracefmt 在跟踪消息到达缓冲区时显示这些消息。 **-O** 参数指定输出文件的位置。

```
tracefmt -rt MyTrace -p c:\tracing -display -o mytrace.txt
```

有关详细示例，请参阅 [示例5：格式 Real-Time 跟踪会话](example-5--formatting-real-time-trace-sessions.md)。

 

 






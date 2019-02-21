---
title: 示例 5 的格式设置实时跟踪会话
description: 示例 5 的格式设置实时跟踪会话
ms.assetid: 340453ab-4736-4191-b9d4-08ee7d9190fe
keywords:
- Tracefmt WDK，实时跟踪会话
- 实时跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f27ca23fe8c86b7f62b523a0fb8d919b256d9ec8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519358"
---
# <a name="example-5-formatting-real-time-trace-sessions"></a>示例 5:格式设置实时跟踪会话


可以从实时跟踪会话除了跟踪日志文件格式的跟踪消息中使用 Tracefmt。

命令使用以下一系列[Tracelog](tracelog.md)和 Tracefmt。 第一个命令使用 Tracelog Tracedrv 示例跟踪提供程序与启动实时跟踪会话。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)，为软件跟踪设计的一个示例驱动程序现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507 )GitHub 上的存储库。

```
tracelog -start MyTrace -guid tracedrv.ctl -flag 1 -rt
```

此命令启动名为 MyTrace 跟踪会话。 它使用-**guid**参数来标识跟踪提供程序，Tracedrv.sys，通过使用其控件 GUID 文件 tracedrv.ctl。 它使用 **-标志**参数设置[跟踪标志](trace-flags.md)值设为**1**。 它使用 **-rt**参数来启动跟踪会话的消息将直接传递到跟踪使用者，如 Tracefmt。 无需 **-rt**参数，跟踪提供程序将消息只发送到日志文件。

下一个命令使用 Tracefmt 设置 Tracedrv MyTrace 跟踪会话期间生成的消息的格式。

```
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt
```

此 Tracefmt 命令使用 **-rt**参数来标识实时跟踪会话，MyTrace，并 **-p**参数来指定 Tracedrv.sys TMF 文件所在的目录。 **-O**参数将输出定向到本地目录中的 mytrace.txt 文件。

此命令的响应，Tracefmt 准备设置实时跟踪消息的格式。 它显示以下状态消息，但不会返回到命令提示符：

```
c:\tracetools>tracefmt -rt mytrace -display -o mytrace.txt
Setting RealTime mode for  mytrace
Getting guids from c:\tracetools\default.tmf
```

以下 Tracelog 命令停止 MyTrace 跟踪会话。 必须在不同的命令提示符窗口中键入该命令。

```
tracelog -stop mytrace
```

当停止跟踪会话时，Tracefmt 报告它已跟踪消息写入到输出文件，然后返回到命令提示符。

```
Event traces dumped to mytrace.txt
Event Summary dumped to mytrace.txt.sum
```

 

 






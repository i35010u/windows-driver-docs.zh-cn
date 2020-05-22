---
title: 示例5格式化实时跟踪会话
description: 示例5格式化实时跟踪会话
ms.assetid: 340453ab-4736-4191-b9d4-08ee7d9190fe
keywords:
- Tracefmt WDK，实时跟踪会话
- 实时跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e13b16211e937a9dd5b9681c3070d9850413b302
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769695"
---
# <a name="example-5-formatting-real-time-trace-sessions"></a>示例5：格式化实时跟踪会话


除了跟踪日志文件之外，还可以使用 Tracefmt 从实时跟踪会话中格式化跟踪消息。

下面的一系列命令使用[Tracelog](tracelog.md)和 Tracefmt。 第一个命令使用 Tracelog 通过 Tracedrv 示例跟踪提供程序启动实时跟踪会话。 [TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)是设计用于软件跟踪的示例驱动程序，位于 GitHub 上的[Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)存储库中。

```
tracelog -start MyTrace -guid tracedrv.ctl -flag 1 -rt
```

此命令启动一个名为 MyTrace 的跟踪会话。 它使用-**guid**参数来标识跟踪提供程序 Tracedrv，方法是使用其控件 guid 文件 Tracedrv。 它使用 **-标志**参数将[跟踪标志](trace-flags.md)值设置为**1**。 它使用 **-rt**参数启动跟踪会话，将消息直接传递到跟踪使用者，如 Tracefmt。 如果不使用 **-rt**参数，则跟踪提供程序只会将消息发送到日志文件。

下一条命令使用 Tracefmt 在 MyTrace 跟踪会话期间对 Tracedrv 生成的消息进行格式设置。

```
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt
```

此 Tracefmt 命令使用 **-rt**参数来标识实时跟踪会话、MyTrace 和 **-p**参数，以指定 Tracedrv 的 TMF 文件所在的目录。 **-O**参数将输出定向到本地目录中的 mytrace 文件。

在此命令中，Tracefmt 准备实时格式化跟踪消息。 它显示以下状态消息，但不返回命令提示符：

```
c:\tracetools>tracefmt -rt mytrace -display -o mytrace.txt
Setting RealTime mode for  mytrace
Getting guids from c:\tracetools\default.tmf
```

以下 Tracelog 命令停止 MyTrace 跟踪会话。 你必须在不同的命令提示符窗口中键入命令。

```
tracelog -stop mytrace
```

跟踪会话停止后，Tracefmt 会报告它将跟踪消息写入输出文件，然后返回到命令提示符。

```
Event traces dumped to mytrace.txt
Event Summary dumped to mytrace.txt.sum
```

 

 






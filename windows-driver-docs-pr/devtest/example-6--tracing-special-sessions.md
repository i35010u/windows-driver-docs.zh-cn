---
title: 示例 6 跟踪特殊会话
description: 示例 6 跟踪特殊会话
ms.assetid: 5e528086-812c-478b-a2d1-69d54781cbb2
keywords:
- Tracefmt WDK，特殊会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f43daa3857a69dca363726e2e5e6c7f060115f17
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380613"
---
# <a name="example-6-tracing-special-sessions"></a>示例 6：跟踪特殊会话


可以使用 Tracefmt 设置 NT 内核记录器，WMI 事件记录器中的跟踪消息的格式和全局记录器保留跟踪会话。

以下命令设置格式并显示从 NT 内核记录器实时跟踪会话的跟踪消息。 (有关启动 NT 内核记录器跟踪会话的信息，请参阅[TraceView](traceview.md)或[Tracelog](tracelog.md)。)

```
tracefmt -rt -tmf system.tmf -display
```

此命令不包括跟踪会话的名称，即使它使用也是如此 **-rt**参数。 它不需要在这种情况下，因为"NT 内核记录器"是默认值。

但是， **-tmf**参数才能将 Tracefmt 定向到 system.tmf 文件。 默认情况下，Tracefmt 使用 default.tmf，不包括格式设置的 NT 内核记录器跟踪消息的说明。 **-P**参数仅当 TMF 文件名称是消息的 guid，如 37753236-c81f-505e-d40a-128d3bb2b5ff.tmf 时查找 TMF 文件。

此命令还使用 **-显示**参数，除了写入日志文件在命令提示符窗口中显示跟踪消息。 在这种情况下，因为 **-o**省略参数，则消息将写入到默认日志文件中，FmtFile.txt，本地目录中。

 

 






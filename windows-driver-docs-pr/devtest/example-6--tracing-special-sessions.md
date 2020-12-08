---
title: 示例6跟踪特殊会话
description: 示例6跟踪特殊会话
keywords:
- Tracefmt WDK，特殊会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: decd8def413728b069b9a42fe022ec0114200a5f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804283"
---
# <a name="example-6-tracing-special-sessions"></a>示例 6：跟踪特殊会话


你可以使用 Tracefmt 来设置来自 NT 内核记录器、WMI 事件记录器和全局记录器保留跟踪会话的跟踪消息的格式。

以下命令将设置和显示来自 NT 内核记录器实时跟踪会话的跟踪消息。  (有关启动 NT 内核记录器跟踪会话的信息，请参阅 [TraceView](traceview.md) 或 [Tracelog](tracelog.md)。 ) 

```
tracefmt -rt -tmf system.tmf -display
```

此命令不包括跟踪会话的名称，即使它使用 **-rt** 参数也是如此。 这不是必需的，因为 "NT 内核记录器" 是默认值。

但是，若要将 Tracefmt 定向到 tmf 文件，需要 **-tmf** 参数。 默认情况下，Tracefmt 使用 tmf，后者不包括 NT 内核记录器跟踪消息的格式说明。 仅当 TMF 文件名为消息 guid，例如 37753236-c81f-505e-d40a-128d3bb2b5ff TMF 时， **-p** 参数才会查找 TMF 文件。

此命令还使用 **-display** 参数，该参数会在命令提示符窗口中显示跟踪消息，并将跟踪消息写入日志文件。 在这种情况下，因为省略了 **-o** 参数，则会将消息写入 FmtFile.txt 本地目录中的默认日志文件。

 

 






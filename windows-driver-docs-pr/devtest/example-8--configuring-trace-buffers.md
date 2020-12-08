---
title: 示例8配置跟踪缓冲区
description: 示例8配置跟踪缓冲区
keywords:
- 跟踪缓冲区 WDK
- 缓冲 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e99735a1528ef3120abd95da9ebd059d9002e6e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804309"
---
# <a name="example-8-configuring-trace-buffers"></a>示例 8：配置跟踪缓冲区


## <span id="ddk_configuring_trace_buffers_tools"></span><span id="DDK_CONFIGURING_TRACE_BUFFERS_TOOLS"></span>


以下命令将启动跟踪日志会话并自定义会话的缓冲区：

```
tracelog -start MyTrace -guid MyProvider.guid -f testtrace.etl -flag 2 -level ffff -b 128 -min 10 -max 30
```

命令启动名为 "MyTrace" 的会话。 它使用 **-guid** 参数指定提供程序文件，并使用 **-f** 参数指定跟踪日志的名称和位置。

它使用 **-标志** 参数将标志值设置为2，并使用 **级别** 参数将级别值设置为 FFFF，这会生成所有可用的跟踪消息。 这些设置特定于提供程序。

为了适应高消息速率，此命令使用 **-b** 参数将每个缓冲区的大小增加到 128 KB **，将最** 小缓冲区数增加到最小值，将最小缓冲区数增加到最大值， **最大值** 为30。

在响应中，Tracelog 启动一个跟踪会话并显示几个会话属性。 此命令设置的属性以粗体显示，便于识别。

```
Logger Started...
Enabling trace to logger 2
Operation Status:       0L      The operation completed successfully.

Logger Name:            MyTrace
Logger Id:              2
Logger Thread Id:       00000D7C
Buffer Size:            128 Kb
Maximum Buffers:        30
Minimum Buffers:        10
Number of Buffers:      10
Free Buffers:           9
Buffers Written:        1
Events Lost:            0
Log Buffers Lost:       0
Real Time Buffers Lost: 0
AgeLimit:               15
Log File Mode:          Sequential
Enabled tracing:        0x00000002
Log Filename:           d:\traces\testtrace.etl 
```

监视跟踪会话属性列表中的 **事件丢失** 计数器始终很重要。 如果丢失事件，请重新运行跟踪会话，并增加缓冲区容量 (大小、数量或同时) 两者。 若要查看跟踪会话的属性，请使用 **tracelog-l** 或 **tracelog**_SessionName_。

 

 






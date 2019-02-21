---
title: 示例 8 配置跟踪缓冲区
description: 示例 8 配置跟踪缓冲区
ms.assetid: 7bcc076c-6feb-4660-88d7-dc4206b53dce
keywords:
- 跟踪缓冲区 WDK
- 缓冲区 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeacc40a9306854311cdbb6cefa93d9142553f94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521367"
---
# <a name="example-8-configuring-trace-buffers"></a>示例 8:配置跟踪缓冲区


## <span id="ddk_configuring_trace_buffers_tools"></span><span id="DDK_CONFIGURING_TRACE_BUFFERS_TOOLS"></span>


以下命令开始跟踪日志会话，自缓冲区定义会话：

```
tracelog -start MyTrace -guid MyProvider.guid -f testtrace.etl -flag 2 -level ffff -b 128 -min 10 -max 30
```

该命令启动名为"MyTrace"的会话。 它使用**guid**参数来指定提供程序文件和 **-f**参数指定的名称和跟踪日志的位置。

它使用 **-标志**标志值设置为 2 的参数和 **-级别**参数级别的值设置为 FFFF，生成所有可用的跟踪消息。 这些设置是特定于提供程序。

为了适应高消息速率，此命令将使用 **-b**参数来增加到 128 KB，每个缓冲区的大小 **-最小值**参数增加最小为 10，将的缓冲区数**的最大**参数增加到 30 的缓冲区的最大数目。

在响应中，跟踪日志启动跟踪会话，并显示几个会话属性。 通过该命令设置的属性以便于识别的粗体类型显示。

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

请务必始终观看**事件丢失**计数器跟踪会话属性列表中。 如果导致事件丢失，重新运行增加的缓冲容量 （大小、 数量，或两者） 跟踪会话。 若要查看跟踪会话的属性，请使用**tracelog-l**或 **tracelog-q * * * SessionName*。

 

 






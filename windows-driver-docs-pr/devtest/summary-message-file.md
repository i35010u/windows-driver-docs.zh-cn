---
title: 摘要消息文件
description: 摘要消息文件
ms.assetid: 90d82aee-5836-4f69-8e52-48400e1445cc
keywords:
- Tracefmt WDK，摘要消息文件
- 摘要消息文件 WDK Tracefmt
- 文件 WDK Tracefmt
- .sum 文件
- sum 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dce1d04a7dc1035e0959339aa2e7ff86dde467f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360937"
---
# <a name="summary-message-file"></a>摘要消息文件


## <span id="ddk_summary_message_file_tools"></span><span id="DDK_SUMMARY_MESSAGE_FILE_TOOLS"></span>


摘要消息文件是文本文件，其中包含有关软件跟踪信息。 创建 Tracefmt*摘要消息 (.sum) 文件*之后处理跟踪日志中的消息或跟踪会话。

该摘要消息文件中的统计摘要包括以下数据：

-   处理的缓冲区数

-   处理和丢失的消息数

-   经过的时间，以微秒为单位，跟踪会话

以下统计摘要是组成为表示在跟踪中每个跟踪消息的一个行的表。 表的每个列提供了有关跟踪消息的以下信息：

<span id="EventCount"></span><span id="eventcount"></span><span id="EVENTCOUNT"></span>**EventCount**  
在跟踪中的跟踪消息的实例数。

<span id="EventName"></span><span id="eventname"></span><span id="EVENTNAME"></span>**EventName**  
友好名称[消息 GUID](message-guid.md)的跟踪消息。 默认情况下，一条消息的 GUID 的友好名称是在其中生成跟踪提供程序，该目录的名称，但可以通过使用指定的备选友好名称 **-p**参数运行\_WPP 或 Tracewpp.exe。 有关信息，请参阅运行\_WPP 选项。 (**EventName**具有相同的值中的 %1 变量[跟踪消息前缀](trace-message-prefix.md)。)

<span id="EventType"></span><span id="eventtype"></span><span id="EVENTTYPE"></span>**EventType**  
跟踪消息的友好名称。 默认情况下，跟踪消息的友好名称是代码的源文件和生成的跟踪消息的行号的名称。 (**EventType**具有相同的值中的 %2 变量[跟踪消息前缀](trace-message-prefix.md)。)

<span id="GUID"></span><span id="guid"></span>**GUID**  
消息的跟踪消息的 GUID。

下面的示例显示了由 Tracedrv，检测跟踪的一个示例驱动程序生成 testtrace.etl 跟踪日志的摘要消息文件。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)，为软件跟踪设计的一个示例驱动程序是从可用[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

```
Files Processed:
d:\DDK Tools\tracetools\testtrace.etl
Total Buffers Processed 4
Total Events  Processed 1718
Total Events  Lost      4
Elapsed Time            122 sec
+---------------------------------------------------------------------------------+
|EventCount    EventName    EventType         Guid                                |
+---------------------------------------------------------------------------------+
|         1    Header       Header            68fdd900-4a3e-11d1-84f4-0000f80464e3|
|      1700    tracedrv     tracedrv_c264     37753236-c81f-505e-d40a-128d3bb2b5ff|
|        17    tracedrv     tracedrv_c258     37753236-c81f-505e-d40a-128d3bb2b5ff|
+---------------------------------------------------------------------------------+
```

上述摘要显示 Tracedrv 生成标头消息和两个跟踪消息。 通过生成一个跟踪消息[ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))由行 258 DoTraceMessage 语句生成行 264，另一个语句。 在此跟踪日志中，有 1700年实例的第一个跟踪消息和 17 的第二个跟踪消息的实例。

摘要消息文件主要用于调试软件跟踪和它的格式可能会发生更改。

 

 






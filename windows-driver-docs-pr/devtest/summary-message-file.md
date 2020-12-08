---
title: 摘要消息文件
description: 摘要消息文件
keywords:
- Tracefmt WDK，摘要消息文件
- 摘要消息文件 WDK Tracefmt
- 文件 WDK Tracefmt
- . sum 文件
- sum 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01ea918e5cbe6c441f40cae72a5b906ef1c8055e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820849"
---
# <a name="summary-message-file"></a>摘要消息文件


## <span id="ddk_summary_message_file_tools"></span><span id="DDK_SUMMARY_MESSAGE_FILE_TOOLS"></span>


摘要消息文件是一个文本文件，其中包含有关软件跟踪的信息。 Tracefmt 在处理跟踪日志或跟踪会话中的消息之后 *( 创建摘要消息) 文件。*

摘要消息文件包含统计摘要中的以下数据：

-   已处理的缓冲区数

-   处理和丢失的消息数

-   跟踪会话的运行时间（微秒）

下面的统计摘要是一个表，该表在跟踪中表示的每个跟踪消息中占一行。 表中的每一列都提供有关跟踪消息的下列信息：

<span id="EventCount"></span><span id="eventcount"></span><span id="EVENTCOUNT"></span>**EventCount**  
跟踪消息在跟踪中的实例数。

<span id="EventName"></span><span id="eventname"></span><span id="EVENTNAME"></span>**名**  
跟踪消息的 [消息 GUID](message-guid.md) 的友好名称。 默认情况下，消息 GUID 的友好名称是在其中生成跟踪提供程序的目录的名称，但您可以通过使用 **-p** 参数运行 WPP 或 Tracewpp.exe 来指定备用的友好名称 \_ 。 有关信息，请参阅运行 \_ WPP 选项。  (**事件名称** 与 [跟踪消息前缀](trace-message-prefix.md)中的 %1 变量具有相同的值。 ) 

<span id="EventType"></span><span id="eventtype"></span><span id="EVENTTYPE"></span>**EventType**  
跟踪消息的友好名称。 默认情况下，跟踪消息的友好名称是源文件的名称和生成跟踪消息的代码的行号。  (**事件** 1 与 [跟踪消息前缀](trace-message-prefix.md)中的 %2 变量具有相同的值。 ) 

<span id="GUID"></span><span id="guid"></span>**GUID.EMPTY**  
跟踪消息的消息 GUID。

下面的示例演示由 Tracedrv 生成的 testtrace 跟踪日志的摘要消息文件，该文件是一个用于跟踪的示例驱动程序。 [TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)是设计用于软件跟踪的示例驱动程序，可从 GitHub 上的 [Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples) 存储库获取。

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

上述摘要显示 Tracedrv 生成标头消息和两条跟踪消息。 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))语句在第264行生成一个跟踪消息，另一个跟踪消息由第258行的 DoTraceMessage 语句生成。 在此跟踪日志中，有1700个实例的第一个跟踪消息和17个实例的第二个跟踪消息。

摘要消息文件主要用于调试软件跟踪，其格式可能会更改。

 


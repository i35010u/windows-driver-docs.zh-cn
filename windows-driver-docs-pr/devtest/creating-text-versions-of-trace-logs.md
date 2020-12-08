---
title: 创建跟踪日志的文本版本
description: 创建跟踪日志的文本版本
keywords:
- TraceView WDK，文本版本跟踪日志
- 跟踪日志 WDK TraceView，文本版本
- 日志文件 WDK TraceView，文本版本
- 跟踪消息列表 WDK
- 文本格式跟踪日志 WDK
- 列出文件 WDK 软件跟踪
- out 文件
- out 文件
- 转换跟踪日志格式
- 格式化 WDK 音频、跟踪日志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46d92e935da4f920bdc19e673cc86def34fe99d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795627"
---
# <a name="creating-text-versions-of-trace-logs"></a>创建跟踪日志的文本版本


跟踪日志会话过程中生成的跟踪消息保存在 [跟踪日志](trace-log.md)中，这些日志是用于有效存储大量跟踪消息的二进制文件。 TraceView 提供了几种便捷的方法来创建这些文件的可读版本。

### <a name="span-idcreating_a_listing_file_for_a_real_time_trace_sessionspanspan-idcreating_a_listing_file_for_a_real_time_trace_sessionspancreating-a-listing-file-for-a-real-time-trace-session"></a><span id="creating_a_listing_file_for_a_real_time_trace_session"></span><span id="CREATING_A_LISTING_FILE_FOR_A_REAL_TIME_TRACE_SESSION"></span>为实时跟踪会话创建列表文件

" **创建列表文件** " 选项将创建一个 *列表文件* ( out) ，该文件是在会话期间生成的所有跟踪消息的文本文件。 仅当创建跟踪会话时，才能使用此选项。 若要为实时跟踪会话创建列表文件，请执行以下操作：

1.  从 " **文件** " 菜单中选择 " **创建新的日志会话**"。

2.  添加提供程序，然后单击 " **下一步**"。

3.  在 " **日志会话选项** " 页面上，单击 " **高级日志会话选项**"。

4.  在 " **输出文件** " 选项卡中，单击 " **创建列表文件**"。

有关详细信息，请参阅 [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)

### <a name="span-idcreating_a_listing_file_for_an_existing_log_filespanspan-idcreating_a_listing_file_for_an_existing_log_filespancreating-a-listing-file-for-an-existing-log-file"></a><span id="creating_a_listing_file_for_an_existing_log_file"></span><span id="CREATING_A_LISTING_FILE_FOR_AN_EXISTING_LOG_FILE"></span>为现有日志文件创建列表文件

启动跟踪日志会话时，可以使用 " **创建列表文件** " 选项创建跟踪日志的文本版本。 若要为现有日志文件创建列表文件，请执行以下操作：

1.  在 " **文件** " 菜单上，单击 " **打开现有日志文件**"。

2.  在 " **日志文件选择** " 对话框中，选择 " **创建列表文件**"。

3.  在 " **日志文件名称** " 框中，指定现有事件跟踪日志 ( .etl) 文件的名称。

显示跟踪日志时，TraceView 将创建列表文件。 有关详细信息，请参阅 [设置跟踪日志选项](setting-trace-log-options.md)。

有关详细信息，请参阅 [**TraceView**](traceview--process.md)。

### <a name="span-idcopying_the_trace_message_listspanspan-idcopying_the_trace_message_listspan-copying-the-trace-message-list"></a><span id="copying_the_trace_message_list"></span><span id="COPYING_THE_TRACE_MESSAGE_LIST"></span> 复制跟踪消息列表

您可以直接从跟踪消息列表中为现有跟踪日志或运行跟踪会话复制跟踪消息。

此过程使您可以最大程度地控制显示器。 可以在对 [跟踪会话进行分组](grouping-trace-sessions.md)之后复制消息，选择要显示的列 ("跟踪消息) 属性"，并对跟踪消息进行排序和筛选。 您还可以从显示中选择单个消息。 若要从跟踪消息列表复制跟踪消息，请执行以下操作：

1.  选择要复制的跟踪消息。 你可以使用 SHIFT + 单击来选择连续消息，或按 CTRL + 单击来复制不连续的消息。

2.  按 CTRL + C。 或者，右键单击任意选定消息的任何单元，然后单击 " **复制**"。

消息是以制表符分隔的格式复制的。 可以将其粘贴到文本文件或电子表格文件中，以便进行保存和分析。

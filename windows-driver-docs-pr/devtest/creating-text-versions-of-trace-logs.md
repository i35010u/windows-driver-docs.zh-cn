---
title: 创建跟踪日志的文本版本
description: 创建跟踪日志的文本版本
ms.assetid: 15d15da3-e381-4b5f-81f2-300aa87e11db
keywords:
- TraceView WDK 文本版本跟踪日志
- 跟踪日志 WDK TraceView，文本版本
- 日志文件 WDK TraceView，文本版本
- 跟踪消息列表 WDK
- 文本格式跟踪日志 WDK
- 列出文件 WDK 软件跟踪
- .out 文件
- 出文件
- 将跟踪日志格式转换
- 格式 WDK 音频，跟踪日志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb57c669a68a71656e5e7cb1a40ac6ffa517d60d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356635"
---
# <a name="creating-text-versions-of-trace-logs"></a>创建跟踪日志的文本版本


在跟踪日志会话过程中生成的跟踪消息保存在[跟踪日志](trace-log.md)，这是用于高效地存储跟踪消息量很大的二进制文件。 TraceView 有几个便利的方法，用于创建这些文件的用户可读版本。

### <a name="span-idcreatingalistingfileforarealtimetracesessionspanspan-idcreatingalistingfileforarealtimetracesessionspancreating-a-listing-file-for-a-real-time-trace-session"></a><span id="creating_a_listing_file_for_a_real_time_trace_session"></span><span id="CREATING_A_LISTING_FILE_FOR_A_REAL_TIME_TRACE_SESSION"></span>为实时跟踪会话创建列表文件

**创建列表文件**选项创建*列表文件*(.out) 在会话期间生成的所有跟踪消息的文本文件。 可以使用此选项仅在创建跟踪会话时。 若要创建实时跟踪会话列表文件，执行以下操作：

1.  从**文件**菜单中，选择**新建日志会话**。

2.  添加提供程序，然后依次**下一步**。

3.  在中**日志会话选项**页上，单击**高级日志会话选项**。

4.  在中**输出文件**选项卡上，单击**创建列表文件**。

有关详细信息，请参阅[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)

### <a name="span-idcreatingalistingfileforanexistinglogfilespanspan-idcreatingalistingfileforanexistinglogfilespancreating-a-listing-file-for-an-existing-log-file"></a><span id="creating_a_listing_file_for_an_existing_log_file"></span><span id="CREATING_A_LISTING_FILE_FOR_AN_EXISTING_LOG_FILE"></span>创建列表文件现有的日志文件

在从开始跟踪日志会话，可以使用**创建列表文件**选项来创建跟踪日志的文本版本。 若要创建列表文件现有的日志文件，请执行以下操作：

1.  上**文件**菜单上，单击**打开现有日志文件**。

2.  在中**日志文件选择**对话框中，选择**创建列表文件**。

3.  在中**日志文件名称**框中，指定现有的事件跟踪日志 (.etl) 文件的名称。

当显示跟踪日志时，TraceView 创建列表文件。 有关详细信息，请参阅[设置跟踪日志选项](setting-trace-log-options.md)。

有关详细信息，请参阅[ **TraceView-进程**](traceview--process.md)。

### <a name="span-idcopyingthetracemessagelistspanspan-idcopyingthetracemessagelistspan-copying-the-trace-message-list"></a><span id="copying_the_trace_message_list"></span><span id="COPYING_THE_TRACE_MESSAGE_LIST"></span> 复制跟踪消息列表

可以将跟踪消息复制直接从现有的跟踪日志或正在运行的跟踪会话的跟踪消息列表。

此过程用于为你显示了最大控制。 您可以将这些消息复制后[分组跟踪会话](grouping-trace-sessions.md)、 选择你想要显示的列 （即，跟踪消息属性） 和排序和筛选跟踪消息。 您还可以从显示中选择各个消息。 要复制跟踪消息从跟踪消息列表，请执行以下操作：

1.  选择你想要复制的跟踪消息。 可以使用 SHIFT + 单击选择连续消息或 CTRL + 单击以复制非连续的邮件。

2.  按 CTRL + C。 或者，右键单击所选的任何任何的消息单元格，并单击**复制**。

这些消息将复制的制表符分隔格式。 可以将其粘贴到文本文件或电子表格文件以保存和分析。

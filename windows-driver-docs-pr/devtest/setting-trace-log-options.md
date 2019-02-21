---
title: 设置跟踪日志选项
description: 设置跟踪日志选项
ms.assetid: 3790a3af-69bd-4ccc-a116-0df6312f378a
keywords:
- 摘要消息文件 WDK TraceView
- 列出消息文件 WDK
- 跟踪日志 WDK TraceView，设置选项
- 日志文件 WDK TraceView，设置选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ade6590e6fd373ae9d21d6f7f849ad15e2f0482
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522189"
---
# <a name="setting-trace-log-options"></a>设置跟踪日志选项


显示跟踪日志时，您还可以创建列表文件或摘要文件。 这些文本文件可以显示和轻松地操作日志数据。 若要设置跟踪日志选项，请使用以下过程：

1.  上**文件**菜单上，单击**打开现有日志文件**。

2.  在中**日志文件选择**对话框中**日志文件选项**区域中，选择跟踪日志选项。

以下列表描述了跟踪日志选项：

<span id="Create_Listing_File"></span><span id="create_listing_file"></span><span id="CREATE_LISTING_FILE"></span>**创建列表文件**  
从实时跟踪会话创建的跟踪消息的格式、 可读文本文件版本或[跟踪日志](trace-log.md)。

在关联的文本框中，键入列表文件的路径和文件名称。 默认值是"LogSession*N*"，其中*N*是一个从零开始的整数，它表示在其中创建该会话的顺序。

<span id="Create_Summary_File"></span><span id="create_summary_file"></span><span id="CREATE_SUMMARY_FILE"></span>**创建摘要文件**  
生成实时跟踪会话或跟踪日志统计信息的文本文件。

在关联的文本框中，键入摘要文件的路径和文件名称。 默认值是"LogSession*N*"，其中*N*是一个从零开始的整数，它表示在其中创建该会话的顺序。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

如果指定现有列表或摘要文件，TraceView 将覆盖该文件而不发出警告。

停止跟踪会话时，TraceView 创建摘要文件。 如果在停止跟踪会话之前关闭 TraceView 窗口，TraceView 不为会话创建摘要文件。

 

 






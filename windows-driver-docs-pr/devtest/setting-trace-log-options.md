---
title: 设置跟踪日志选项
description: 设置跟踪日志选项
keywords:
- 摘要消息文件 WDK TraceView
- 列出消息文件 WDK
- 跟踪日志 WDK TraceView，设置选项
- 日志文件 WDK TraceView，设置选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa789cbd21f358d9759ebbd383e6207ddd44338d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828817"
---
# <a name="setting-trace-log-options"></a>设置跟踪日志选项


显示跟踪日志时，还可以创建列表文件或摘要文件。 这些文本文件使你可以轻松地显示和操作日志数据。 若要设置跟踪日志选项，请使用以下过程：

1.  在 " **文件** " 菜单上，单击 " **打开现有日志文件**"。

2.  在 " **日志文件选择** " 对话框的 " **日志文件选项** " 区域中，选择 "跟踪日志选项"。

以下列表描述了跟踪日志选项：

<span id="Create_Listing_File"></span><span id="create_listing_file"></span><span id="CREATE_LISTING_FILE"></span>**创建列表文件**  
从实时跟踪会话或 [跟踪日志](trace-log.md)创建跟踪消息的格式的可读文本文件版本。

在关联的文本框中，键入列表文件的路径和文件名。 默认值为 "LogSession *n*"，其中 *N* 是一个从零开始的整数，它表示会话的创建顺序。

<span id="Create_Summary_File"></span><span id="create_summary_file"></span><span id="CREATE_SUMMARY_FILE"></span>**创建摘要文件**  
生成有关实时跟踪会话或跟踪日志的统计信息的文本文件。

在关联的文本框中，键入摘要文件的路径和文件名。 默认值为 "LogSession *n*"，其中 *N* 是一个从零开始的整数，它表示会话的创建顺序。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

如果指定现有列表或摘要文件，TraceView 将在不发出警告的情况下覆盖该文件。

当你停止跟踪会话时，TraceView 将创建摘要文件。 如果在停止跟踪会话前关闭 TraceView 窗口，则 TraceView 不会为会话创建摘要文件。

 

 






---
title: 输出文件选项
description: 输出文件选项
keywords:
- 跟踪会话 WDK，高级选项
- 摘要消息文件 WDK TraceView
- 列出文件 WDK
- 输出文件 WDK TraceView
- 文件 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de25452922a974721eeb341201669470b953a525
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840789"
---
# <a name="output-file-options"></a>输出文件选项


在 " **输出文件** " 选项卡中，您可以为 [跟踪会话](trace-session.md)创建文本文件。 只能在创建跟踪会话时设置和更改以下选项。 会话启动后，不能更改这些选项。

<span id="Create_Listing_File"></span><span id="create_listing_file"></span><span id="CREATE_LISTING_FILE"></span>**创建列表文件**  
从实时跟踪会话或 [跟踪日志](trace-log.md)创建跟踪消息的格式的可读文本文件版本。

在关联的文本框中，键入列表文件的路径和文件名。 默认情况下，在本地目录中为 LogSession *n*，其中 *N* 是一个从零开始的整数，它表示创建会话的顺序。

<span id="Create_Summary_File"></span><span id="create_summary_file"></span><span id="CREATE_SUMMARY_FILE"></span>**创建摘要文件**  
生成有关实时跟踪会话或跟踪日志的统计信息的文本文件。

在关联的文本框中，键入摘要文件的路径和文件名。 默认值 *为 LogSession 中* 的 sum，其中 *n* 是一个从零开始的整数，它表示创建会话的顺序。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

这些选项仅适用于正在创建的跟踪会话，即使在跟踪会话组中包含跟踪会话也是如此。 组中的跟踪会话不共享其跟踪会话选项。

如果指定现有输出文件或摘要文件的路径和文件名，则 TraceView 会在不发出警告的情况下覆盖该文件。

当你停止跟踪会话时，TraceView 将创建摘要文件。 如果在停止跟踪会话前关闭 TraceView 窗口，则 TraceView 不会为会话创建摘要文件。

 

 






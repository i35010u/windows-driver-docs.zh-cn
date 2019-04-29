---
title: 输出文件选项
description: 输出文件选项
ms.assetid: f53785d8-2a91-47da-945c-8c52d6345ae9
keywords:
- 跟踪会话 WDK，高级选项
- 摘要消息文件 WDK TraceView
- 列出文件 WDK
- 输出文件 WDK TraceView
- 文件 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24c3fd226dc1906d7d729bfc5ac39a9a77e32ffe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356351"
---
# <a name="output-file-options"></a>输出文件选项


在中**输出文件**选项卡上，可以创建文本文件供[跟踪会话](trace-session.md)。 可以设置并更改只有在创建跟踪会话时，以下选项。 会话启动后，您不能更改这些选项。

<span id="Create_Listing_File"></span><span id="create_listing_file"></span><span id="CREATE_LISTING_FILE"></span>**创建列表文件**  
从实时跟踪会话创建的跟踪消息的格式、 可读文本文件版本或[跟踪日志](trace-log.md)。

在关联的文本框中，键入列表文件的路径和文件名称。 默认值是 LogSession*N*.out 在本地目录中，其中*N*是一个从零开始的整数，它表示在其中创建该会话的顺序。

<span id="Create_Summary_File"></span><span id="create_summary_file"></span><span id="CREATE_SUMMARY_FILE"></span>**创建摘要文件**  
生成实时跟踪会话或跟踪日志统计信息的文本文件。

在关联的文本框中，键入摘要文件的路径和文件名称。 默认值是 LogSession*N*.sum 在本地目录中，其中*N*是一个从零开始的整数，它表示在其中创建该会话的顺序。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

这些选项仅适用于要创建跟踪会话即使跟踪会话组中包括跟踪会话。 在组中的跟踪会话不共享其跟踪会话选项。

如果指定现有的输出或摘要文件的路径和文件名称，TraceView 将覆盖该文件而不发出警告。

停止跟踪会话时，TraceView 创建摘要文件。 如果在停止跟踪会话之前关闭 TraceView 窗口，TraceView 不为会话创建摘要文件。

 

 






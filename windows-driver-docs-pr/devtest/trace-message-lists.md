---
title: 跟踪消息列表
description: 跟踪消息列表
ms.assetid: 32dcd09d-1046-4785-91bc-ccdd79452c7d
keywords:
- TraceView WDK、 窗口
- 跟踪消息列表 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a75ff6e1d6490d3cf1d8b2ab41f533e05ff642a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565353"
---
# <a name="trace-message-lists"></a>跟踪消息列表


TraceView 显示之一*跟踪消息列表*为每个跟踪会话或跟踪日志[跟踪会话列表](trace-session-list.md)。 跟踪消息列表可能为空，例如跟踪会话首先开始时，也可能包含大量跟踪消息。

下面的屏幕截图显示了一个跟踪会话列表，其中显示两个现有的日志： 一个用于 Tracedrv，这是一个示例跟踪检测驱动程序包含在 WDK 中，和一个用于[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。 为每个跟踪会话没有一个跟踪消息列表。

![显示 tracedrv 和 nt 内核记录器跟踪会话日志跟踪会话列表的屏幕截图](images/traceview-multilog.png)

左边框的每个跟踪消息列表上的会话 Id 可帮助您将跟踪消息列表与跟踪会话相关联。 在此示例中，顶部的跟踪消息列表，其名称为"ID 0"，对应于会话 0，即*LogSession0*; 显示 Tracedrv.etl 日志跟踪会话列表中的会话。

底部名为"ID 1"的跟踪消息列表对应于会话 1，这是 LogSession1;跟踪会话列表中显示的 NTKernelLogger.etl 日志会话。

以下主题介绍的内容和跟踪消息列表的功能：

[跟踪消息列表列](trace-message-list-columns.md)

[跟踪消息列表的功能](trace-message-list-features.md)

 

 






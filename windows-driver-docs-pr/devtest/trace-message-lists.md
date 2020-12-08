---
title: 跟踪消息列表
description: 跟踪消息列表
keywords:
- TraceView WDK，窗口
- 跟踪消息列表 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af3a0daf651d31d1a9769799f257fc98455b2a04
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788733"
---
# <a name="trace-message-lists"></a>跟踪消息列表


TraceView 为 [跟踪会话列表](trace-session-list.md)中的每个跟踪会话或跟踪日志显示一个 *跟踪消息列表*。 跟踪消息列表可能为空，例如跟踪会话首次启动时，或可能包含大量跟踪消息。

下面的屏幕截图显示了一个跟踪会话列表，其中显示了两个现有日志：一个用于 Tracedrv，它是一种包含在 WDK 中的示例跟踪检测驱动程序，另一个用于 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。 每个跟踪会话有一个跟踪消息列表。

![显示 tracedrv 和 nt 内核记录器跟踪会话日志的跟踪会话列表的屏幕截图](images/traceview-multilog.png)

每个跟踪消息列表左边框的会话 Id 有助于将跟踪消息列表与跟踪会话关联。 在此示例中，名为 "ID 0" 的顶部跟踪消息列表对应于 session 0，后者为 *LogSession0*;在跟踪会话列表中显示 Tracedrv 日志的会话。

底部跟踪消息列表（名为 "ID 1"）对应于会话1，后者为 LogSession1;在跟踪会话列表中显示 NTKernelLogger 日志的会话。

以下主题描述跟踪消息列表的内容和功能：

[跟踪消息列表列](trace-message-list-columns.md)

[跟踪消息列表功能](trace-message-list-features.md)

 

 






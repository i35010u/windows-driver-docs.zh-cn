---
title: 跟踪标志
description: 跟踪标志
ms.assetid: a94159ab-ce21-4604-beb8-ee01e333505e
keywords:
- 跟踪标志 WDK
- 标志 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fad3585b2e31b2d95eb0b9a0e52ece0de633d5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339724"
---
# <a name="trace-flags"></a>跟踪标志


跟踪标志是属性的[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序。 这些标志确定跟踪提供程序生成的事件。 提供程序将解释为用于生成消息的条件的标志。

通常情况下，标志表示越来越详细的报告级别，但该提供程序可以使用标记来表示用于生成的跟踪消息的任何条件。

跟踪提供程序定义每个标记中 WPP\_定义\_位元素[WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)结构。 Windows 软件跟踪预处理器 (WPP) 将位值分配给它们在结构中，显示的顺序中的元素从 1 开始。

运行时[跟踪会话](trace-session.md)，可以使用跟踪标志以确定哪些消息将在会话期间生成。 [跟踪使用者](trace-consumer.md)，如[Tracelog](tracelog.md)并[TraceView](traceview.md)，可让用户设置参数和选项，以选择的跟踪标志和[跟踪级别](trace-level.md)为每个中的跟踪会话提供程序。

重新启用跟踪提供程序运行的跟踪会话时，您可以更改的跟踪标志。

 

 






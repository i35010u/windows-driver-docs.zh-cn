---
title: 跟踪标志
description: 跟踪标志
ms.assetid: a94159ab-ce21-4604-beb8-ee01e333505e
keywords:
- 跟踪标志 WDK
- 标志 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2d42309c449b06f2e82e047c5d91968bc4efc1e
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384143"
---
# <a name="trace-flags"></a>跟踪标志


跟踪标志是 [跟踪提供程序](trace-provider.md)的属性，例如内核模式驱动程序或用户模式应用程序。 这些标志确定跟踪提供程序生成的事件。 提供程序将标志解释为生成消息的条件。

通常，标志表示越来越详细的报表级别，但提供程序可以使用标志来表示生成跟踪消息的任何条件。

跟踪提供程序定义 WPP \_ \_ [ \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 结构的 wpp 定义位元素中的每个标志。 Windows 软件跟踪预处理器 (WPP) 按照从1开始的结构中显示的顺序向元素分配位值。

运行 [跟踪会话](trace-session.md)时，可以使用跟踪标志来确定在会话过程中将生成哪些消息。 [跟踪使用者](trace-consumer.md)（例如 [Tracelog](tracelog.md) 和 [TraceView](traceview.md)）允许用户设置参数和选项，以便为跟踪会话中的每个提供程序选择跟踪标志和 [跟踪级别](trace-level.md) 。

可以通过重新启用跟踪提供程序，在运行跟踪会话时更改跟踪标志。

 


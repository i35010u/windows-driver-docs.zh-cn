---
title: 跟踪级别
description: 跟踪级别
ms.assetid: 7ad3f6ee-61a4-4a0e-ab76-d839ae97a2b3
keywords:
- 跟踪级别 WDK
- 级别 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ba052f6d7f2762c2a17e11e1c840608e1fbd2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524524"
---
# <a name="trace-level"></a>跟踪级别


跟踪级别均归[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序。 跟踪级别确定跟踪提供程序生成的事件。 通常情况下，跟踪级别表示 （信息、 警告或错误），该事件的严重性，但跟踪提供程序可以在定义它们来表示用于生成的跟踪消息的任何条件。

与不同[跟踪标志](trace-flags.md)，通过将跟踪提供程序中所定义[WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)结构级别 Evntrace.h，公共标头文件中定义的跟踪。 但是，跟踪提供程序解释级别，并确定其效果

[跟踪使用者](trace-consumer.md)如[Tracelog](tracelog.md)并[TraceView](traceview.md)，将跟踪级别传递给中的提供程序*EnableLevel*参数**EnableTrace**函数。 璝惠**EnableTrace**，请参阅 Microsoft Windows SDK 文档。

跟踪提供程序的开发人员还可以编写自定义的跟踪函数 (的替代方法[ **DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918)) 作为生成的跟踪消息的条件包括跟踪级别。 有关说明，请参阅[我可以自定义 DoTraceMessage？](can-i-customize-dotracemessage-.md)

运行时跟踪会话，用户可以使用的跟踪级别以确定哪些消息将在会话期间生成。 [跟踪使用者](trace-consumer.md)，如[Tracelog](tracelog.md)并[TraceView](traceview.md)，可让用户设置参数和选项，以跟踪会话中每个提供程序选择的跟踪标志和跟踪级别。

跟踪标志，如用户可以重新启用跟踪提供程序运行的跟踪会话时，将跟踪级别更改。

 

 






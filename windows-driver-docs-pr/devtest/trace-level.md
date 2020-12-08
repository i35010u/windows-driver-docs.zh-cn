---
title: 跟踪级别
description: 跟踪级别
keywords:
- 跟踪级别 WDK
- 级别 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1c800c64439141fec076698c04b24548fe86b8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805643"
---
# <a name="trace-level"></a>跟踪级别


跟踪级别是 [跟踪提供程序](trace-provider.md)的属性，例如内核模式驱动程序或用户模式应用程序。 跟踪级别确定跟踪提供程序生成的事件。 通常，跟踪级别表示事件 (信息、警告或错误) 的严重性，但跟踪提供程序可以将它们定义为表示生成跟踪消息的任何条件。

与跟踪标记不同，跟踪 [标志](trace-flags.md)是在 [WPP \_ 控制 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 结构中由跟踪提供程序定义的，跟踪级别是在 Evntrace 中定义的，即公共标头文件。 但是，跟踪提供程序会解释级别并确定其效果

[跟踪使用者](trace-consumer.md)（例如 [Tracelog](tracelog.md)和 [TraceView](traceview.md)）将跟踪级别传递到 **EnableTrace** 函数的 *EnableLevel* 参数中的提供程序。 有关 **EnableTrace** 的信息，请参阅 Microsoft Windows SDK 文档。

跟踪提供程序的开发人员还可以编写自定义的跟踪函数 (替换为包含跟踪级别的 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))) ，以生成跟踪消息。 有关说明，请参阅可否 [自定义 DoTraceMessage？](can-i-customize-dotracemessage-.md)

当运行跟踪会话时，用户可以使用跟踪级别来确定在会话过程中将生成哪些消息。 [跟踪使用者](trace-consumer.md)（例如 [Tracelog](tracelog.md) 和 [TraceView](traceview.md)）允许用户设置参数和选项，以便为跟踪会话中的每个提供程序选择跟踪标志和跟踪级别。

与跟踪标志一样，用户可以通过重新启用跟踪提供程序，在运行跟踪会话时更改跟踪级别。

 


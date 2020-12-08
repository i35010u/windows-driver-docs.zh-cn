---
title: 如何实现更新正在运行的跟踪会话中的标志
description: 如何实现更新正在运行的跟踪会话中的标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50821c3425e033d7260fe2d95bc5e86baebe68bc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792363"
---
# <a name="how-do-i-update-the-flags-in-a-running-trace-session"></a>如何更新正在运行的跟踪会话中的标志？


若要在正在运行的跟踪会话中更改 [跟踪标志](trace-flags.md) 或 [跟踪级别](trace-level.md) ，请使用 **tracelog** 命令，而不是 **tracelog** 命令。 有关详细信息，请参阅 [**Tracelog 命令语法**](tracelog-command-syntax.md)。

标志和级别是 [跟踪提供程序](trace-provider.md)的属性，而不是 [跟踪会话](trace-session.md)的属性。 因此，不能使用 **tracelog 更新** 和更新跟踪会话的命令来更改提供程序的属性。 相反，请使用 **tracelog** 命令，使用新属性重新启用提供程序。

有关 **tracelog** 命令的信息，请参阅 [**tracelog 命令语法**](tracelog-command-syntax.md)。 有关如何使用此命令的示例，请参阅 [示例5：启用跟踪提供程序](example-5--enabling-trace-providers.md)。

还可以使用 [TraceView](traceview.md) 在使用 TraceView 启动的跟踪会话中更改标志或级别。 利用图形用户界面，可以轻松查看在运行会话时可以更改的属性，以及更改这些属性。

 

 






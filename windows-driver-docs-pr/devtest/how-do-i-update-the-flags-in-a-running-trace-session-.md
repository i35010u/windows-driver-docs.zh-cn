---
title: 如何在正在运行的跟踪会话中更新标志
description: 如何在正在运行的跟踪会话中更新标志
ms.assetid: 952cc60f-1877-49d5-b87c-493c1b90cfdf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 467431b21c66864d5dcf018704c030acdf30473b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526092"
---
# <a name="how-do-i-update-the-flags-in-a-running-trace-session"></a>如何在正在运行的跟踪会话中更新标志


若要更改[跟踪标志](trace-flags.md)或[跟踪级别](trace-level.md)在正在运行的跟踪会话，使用**tracelog-启用**未命令**tracelog-更新**命令。 有关详细信息，请参阅[ **Tracelog 命令语法**](tracelog-command-syntax.md)。

标志和级别均归[跟踪提供程序](trace-provider.md)，不是[跟踪会话](trace-session.md)。 因此， **tracelog-更新**，命令以更新跟踪会话中，不能用于更改提供程序的属性。 请改用**tracelog-启用**命令以重新启用具有新属性的提供程序。

璝惠**tracelog-启用**命令，请参阅[ **Tracelog 命令语法**](tracelog-command-syntax.md)。 有关如何使用此命令的示例，请参阅[示例 5:启用跟踪提供程序](example-5--enabling-trace-providers.md)。

此外可以使用[TraceView](traceview.md)通过使用 TraceView 启动跟踪会话中更改的标志或级别。 图形用户界面使我们可以很容易看到哪些属性可以更改在会话运行的同时，并更改它们。

 

 






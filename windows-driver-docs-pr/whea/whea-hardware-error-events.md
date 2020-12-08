---
title: WHEA 硬件错误事件
description: WHEA 硬件错误事件
keywords:
- 事件 WDK WHEA，关于事件
- Windows 硬件错误体系结构 WDK，事件
- WHEA WDK，事件
- 硬件错误 WDK WHEA，事件
- 错误 WDK WHEA，事件
- 硬件错误事件 WDK WHEA
- 事件 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 216283bdf74bc2d3f30e521854054da68fffac2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811297"
---
# <a name="whea-hardware-error-events"></a>WHEA 硬件错误事件


Windows 硬件错误体系结构 (WHEA) 每当发生硬件错误时，就会引发 Windows (ETW) 事件的事件跟踪。 这些硬件错误事件记录在系统事件日志中。 有关 WHEA 可以引发的各种硬件错误事件的说明，请参阅 [硬件错误事件](/windows-hardware/drivers/ddi/_whea/)。

应用程序可以通过查询 WHEA 记录的任何事件，从系统事件日志中检索硬件错误事件。 有关如何从系统事件日志中检索 WHEA 硬件错误事件的示例，请参阅 [查询系统事件日志以查找硬件错误事件](querying-the-system-event-log-for-hardware-error-events.md)。

当 WHEA 引发新硬件错误事件时，应用程序还可以注册以获得通知。 有关如何注册新硬件错误事件通知的示例，请参阅 [注册获得硬件错误事件的通知](registering-for-notification-of-hardware-error-events.md)。

无论是通过查询系统事件日志还是通过接收事件通知来获取特定硬件错误事件，从事件中检索硬件错误数据的过程是相同的。

每个硬件错误事件都包含一条描述发生的错误情况的 [错误记录](error-records.md) 。 可以从每个事件中检索错误记录，以便进行进一步分析。

 


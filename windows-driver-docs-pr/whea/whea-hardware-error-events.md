---
title: WHEA 硬件错误事件
description: WHEA 硬件错误事件
ms.assetid: c9f88e3b-3915-4a77-8d60-f0f3da514abc
keywords:
- 有关事件的事件 WDK WHEA
- Windows 硬件错误体系结构 WDK 事件
- WHEA WDK 事件
- 硬件错误 WDK WHEA，事件
- 错误 WDK WHEA，事件
- 硬件错误事件 WDK WHEA
- WDK WHEA 事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b8226243c435e6aede57631301886e50151a7fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387142"
---
# <a name="whea-hardware-error-events"></a>WHEA 硬件错误事件


Windows 硬件错误体系结构 (WHEA) 引发一个事件跟踪 Windows (ETW) 事件，每当硬件错误发生时。 系统事件日志中记录这些硬件错误事件。 WHEA 会出现的各种硬件错误事件的说明，请参阅[硬件错误事件](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)。

通过查询 WHEA 未记录任何事件，应用程序可以从系统事件日志检索硬件错误事件。 有关如何从系统事件日志中检索 WHEA 硬件错误事件的示例，请参阅[查询硬件错误事件的系统事件日志](querying-the-system-event-log-for-hardware-error-events.md)。

应用程序还可以注册新的硬件错误事件引发的 WHEA 时得到通知。 有关如何注册新的硬件错误事件通知的示例，请参阅[注册硬件错误事件的通知](registering-for-notification-of-hardware-error-events.md)。

无论是否通过查询系统事件日志或通过接收事件通知，已获得特定的硬件错误事件，从事件中检索的硬件错误数据的过程是相同的。

每个硬件错误事件包含[错误记录](error-records.md)，描述发生的错误条件。 错误记录可以检索从每个事件以进行进一步分析。

 

 





---
title: 事件机制和流
description: 事件机制和流
ms.assetid: 13a6c6fb-3615-44ef-bf01-5003520b3e26
keywords:
- 事件操作流 WDK 视频捕获
- 终止扫描 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70ecc41adbc8e9b58d2494221089fa2a00ffab08
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384108"
---
# <a name="event-mechanism-and-flow"></a>事件机制和流


**本部分仅适用于与 Microsoft Windows Vista 一起启动的操作系统。**

扫描操作完成后，驱动程序会通知事件的应用程序处理这种情况**EventData**的成员[ **KSEVENT\_调谐器\_启动\_扫描\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)结构指定。 但是，若要确定此扫描操作，该驱动程序的实际锁状态[ **KSPROPERTY\_调谐器\_扫描\_状态**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status)必须调用属性。

应用程序可以取消所有内核流式处理事件请求，如[ **KSEVENT\_调谐器\_启动\_扫描**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)事件完成之前的事件请求。 当应用程序需要取消的当前扫描操作，调谐器筛选器 (*KsTvTune.ax*) 设置**StartFrequency**并**EndFrequency**成员KSEVENT\_调谐器\_启动\_扫描\_S 将注意力集中在对驱动程序的 KSEVENT\_调谐器\_启动\_扫描。 该驱动程序可能会执行整个清理。 但是，由于*KsTvTune.ax*可能会请求另一整个扫描操作，该驱动程序可能无法执行整个清理。 若要取消扫描操作的调用是同步操作。

当应用程序所需的扫描，终止*KsTvTune.ax*调用 KSEVENT\_调谐器\_启动\_扫描了**StartFrequency**和**EndFrequency**设置为零，以取消注册该事件。 然后，该驱动程序必须执行与其工作线程和其他内部数据结构的整个清理。

 

 





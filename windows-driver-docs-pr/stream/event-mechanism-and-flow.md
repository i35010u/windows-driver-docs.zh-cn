---
title: 事件机制和流
description: 事件机制和流
ms.assetid: 13a6c6fb-3615-44ef-bf01-5003520b3e26
keywords:
- 事件操作流 WDK 视频捕获
- 终止扫描 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76fb8256d748ae13a389e8256916229d68c10441
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834422"
---
# <a name="event-mechanism-and-flow"></a>事件机制和流


**本部分仅适用于从 Microsoft Windows Vista 开始的操作系统。**

当扫描操作完成时，驱动程序将通过一个事件句柄通知应用程序 ，该事件句柄[ **\_\_调谐器的 KSEVENT 成员\_scan 指定的\_扫描**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)。 但是，若要确定扫描操作的实际锁定状态，必须调用驱动程序的[**KSPROPERTY\_调谐器\_scan\_status**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status)属性。

与所有内核流式处理事件请求一样，应用程序可以取消[**KSEVENT\_调谐器\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)在事件完成之前启动\_扫描事件请求。 当应用程序需要取消当前扫描操作时，调谐器筛选器（*KsTvTune.ax*）会将 KSEVENT 的**StartFrequency**和**EndFrequency**成员设置\_调谐器\_启动\_扫描\_S 到零在调用驱动程序的 KSEVENT\_调谐器\_启动\_扫描。 驱动程序可能会执行整个清理。 但是，由于*KsTvTune.ax*可能会请求另一次扫描操作，因此驱动程序可能不会执行整个清理操作。 取消扫描操作的调用是同步操作。

当应用程序需要终止扫描时， *KsTvTune.ax*会调用 KSEVENT\_调谐器\_启动\_SCAN with **StartFrequency** ， **EndFrequency**设置为零，以注销事件。 然后，该驱动程序必须执行其工作线程和其他内部数据结构的整个清理。

 

 





---
title: 事件机制和流
description: 事件机制和流
ms.assetid: 13a6c6fb-3615-44ef-bf01-5003520b3e26
keywords:
- 事件操作流 WDK 视频捕获
- 终止扫描 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa8aa355f1ed9ec7efed0dad5625fb0be9e7730a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188004"
---
# <a name="event-mechanism-and-flow"></a>事件机制和流


**本部分仅适用于从 Microsoft Windows Vista 开始的操作系统。**

当扫描操作完成时，驱动程序会通过一个事件句柄通知应用程序，该事件句柄由[**KSEVENT \_ 调谐器 \_ 发起 \_ 扫描 \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)的**EventData**成员指定。 但是，若要确定扫描操作的实际锁定状态，必须调用驱动程序的 [**KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态**](./ksproperty-tuner-scan-status.md) 属性。

与所有内核流式处理事件请求一样，应用程序可以在事件完成前取消 [**KSEVENT \_ 调谐器 \_ 启动 \_ 扫描**](./ksevent-tuner-initiate-scan.md) 事件请求。 当应用程序需要取消当前扫描操作时，调谐器筛选器 (*KsTvTune.ax*) 将 KSEVENT 调谐器的 **StartFrequency** 和 **EndFrequency** 成员设置 \_ \_ \_ \_ 为在对驱动程序的 KSEVENT \_ 调谐器发起扫描的调用中设置为零 \_ \_ 。 驱动程序可能会执行整个清理。 但是，由于 *KsTvTune.ax* 可能会请求另一次扫描操作，因此驱动程序可能不会执行整个清理操作。 取消扫描操作的调用是同步操作。

当应用程序需要终止扫描时， *KsTvTune.ax* 会调用 KSEVENT \_ 调谐器 \_ INITIATE \_ **StartFrequency** 和 **EndFrequency** 设置为零的扫描，以注销事件。 然后，该驱动程序必须执行其工作线程和其他内部数据结构的整个清理。

 


---
title: 硬件辅助的扫描算法
description: 硬件辅助的扫描算法
ms.assetid: 9a24b985-9667-4424-84e5-b1c728b3c558
keywords:
- 硬件辅助的扫描 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c99aaabcc3f8b327b62eced37328400e160ebec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384016"
---
# <a name="hardware-assisted-scanning-algorithm"></a>硬件辅助的扫描算法


**本部分仅适用于与 Microsoft Windows Vista 一起启动的操作系统。**

驱动程序设置**fSupportsHardwareAssistedScanning**的成员[ **KSPROPERTY\_调谐器\_扫描\_CAPS\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)对的调用中的结构及其[ **KSPROPERTY\_调谐器\_扫描\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-caps)属性以指示它和其相关联的硬件支持基于事件的扫描操作。 调谐器筛选器 (*KsTvTune.ax*) 调用驱动程序的 KSPROPERTY\_调谐器\_扫描\_CAPS 属性来确定该驱动程序是否支持硬件辅助扫描。 调谐器筛选器还会调用 KSPROPERTY\_调谐器\_扫描\_大写字母，以确定广播网络的驱动程序支持扫描的类型。 如果该驱动程序支持硬件辅助扫描，它可以返回扫描功能通过每个受支持的广播的网络类型及其[ **KSPROPERTY\_调谐器\_NETWORKTYPE\_扫描\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-networktype-scan-caps)属性。 包括扫描功能，例如，提供优化的设备需要的设置来进入稳定状态的频率的时间量 （处置时间） 和提供频率范围优化筛选器可用于检测存在可优化信号 （感应范围）。 有关扫描模拟的广播网络的功能的信息，请参阅[**调谐器\_模拟\_CAPS\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tuner_analog_caps_s)结构。

*KsTvTune.ax*近似使用处置时间值。 *KsTvTune.ax*扫描过程可能需要多长时间基于扫描的频率范围和花巨资投入的范围为可以提供具有关闭估计的应用程序。 驱动程序的后[ **KSEVENT\_调谐器\_启动\_扫描**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)事件调用以启动扫描进程、 应用程序可以等待事件规定时间内通知。

对于硬件辅助扫描，具体取决于是否优化设备已锁定到信号，该驱动程序返回任一调谐器\_LockType\_None 或调谐器\_LockType\_锁定到其的调用中的状态[**KSPROPERTY\_调谐器\_扫描\_状态**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status)属性。 如果该驱动程序已锁定到信号，该驱动程序还会返回锁定信号的频率。

 

 





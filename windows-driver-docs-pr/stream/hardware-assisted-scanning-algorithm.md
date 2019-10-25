---
title: 硬件辅助的扫描算法
description: 硬件辅助的扫描算法
ms.assetid: 9a24b985-9667-4424-84e5-b1c728b3c558
keywords:
- 硬件辅助扫描 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85ce3b4466638ce7d71f8b4f214a1bb7f59026b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843354"
---
# <a name="hardware-assisted-scanning-algorithm"></a>硬件辅助的扫描算法


**本部分仅适用于从 Microsoft Windows Vista 开始的操作系统。**

驱动程序将 KSPROPERTY\_调谐器的**fSupportsHardwareAssistedScanning**成员设置为对其[**KSPROPERTY\_调谐器**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-caps)的调用[ **\_扫描\_cap\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)一个属性，用于指示该属性及其关联的硬件支持基于事件的扫描操作。 调谐器筛选器（*KsTvTune.ax*）调用驱动程序的 KSPROPERTY\_调谐器\_SCAN\_cap 属性来确定驱动程序是否支持硬件辅助扫描。 调谐器筛选器还会调用 KSPROPERTY\_调谐器\_扫描\_CAP，以确定驱动程序支持扫描的广播网络类型。 如果驱动程序支持硬件辅助扫描，则它可以通过其[**KSPROPERTY\_调谐器\_NETWORKTYPE\_SCAN\_cap**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-networktype-scan-caps)属性返回每种支持的广播网络类型的扫描功能。 例如，扫描功能包括：提供优化设备需要的时间量设置为稳定（正在优化时间），并提供优化筛选器可用于检测可调状态的状态的频率范围信号（检测范围）。 有关模拟模拟广播网络的扫描功能的信息，请参阅[**调谐器\_模拟\_cap\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tuner_analog_caps_s)结构。

*KsTvTune.ax*将使用 "结算时间" 值作为近似值。 *KsTvTune.ax*可以提供一个应用程序，该应用程序可以根据扫描频率范围和检测范围，对扫描进程可能会花费的时间进行密切估算。 在驱动程序的[**KSEVENT\_调谐器\_启动\_SCAN**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)事件以启动扫描进程后，应用程序可以等待事件通知规定时间。

对于硬件辅助扫描，根据调谐设备是否锁定到信号，驱动程序将返回调谐器\_LockType\_无或调谐器\_LockType\_锁定状态从调用其[**KSPROPERTY\_调谐器\_扫描\_状态**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status)属性。 如果驱动程序已锁定到信号，则驱动程序还会返回锁定信号的频率。

 

 





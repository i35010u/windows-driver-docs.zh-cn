---
title: 硬件辅助的扫描算法
description: 硬件辅助的扫描算法
ms.assetid: 9a24b985-9667-4424-84e5-b1c728b3c558
keywords:
- 硬件辅助扫描 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f89986a9a3a84aefff17249d9bc729398bc54d5d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190569"
---
# <a name="hardware-assisted-scanning-algorithm"></a>硬件辅助的扫描算法


**本部分仅适用于从 Microsoft Windows Vista 开始的操作系统。**

驱动程序会在对其[**KSPROPERTY \_ 调谐器 \_ 扫描 \_ cap**](./ksproperty-tuner-scan-caps.md)属性的调用中设置[**KSPROPERTY \_ 调谐器 \_ 扫描 \_ 端 \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)结构的**fSupportsHardwareAssistedScanning**成员，以指示其及其关联的硬件支持基于事件的扫描操作。 调谐器筛选器 (*KsTvTune.ax*) 调用驱动程序的 KSPROPERTY \_ 调谐器 \_ 扫描 \_ cap 属性来确定驱动程序是否支持硬件辅助扫描。 调谐器筛选器还会调用 KSPROPERTY \_ 调谐器 \_ 扫描 \_ cap 来确定驱动程序支持扫描的广播网络类型。 如果驱动程序支持硬件辅助扫描，则可以通过其 [**KSPROPERTY \_ 调谐器 \_ NETWORKTYPE \_ SCAN \_ cap**](./ksproperty-tuner-networktype-scan-caps.md) 属性返回每种支持的广播网络类型的扫描功能。 例如，扫描功能包括：提供优化设备要求频率设置稳定的时间， (的时间范围内，) 并提供调节筛选器可用于检测是否存在可优化信号 (检测范围) 的频率范围。 有关模拟模拟广播网络的扫描功能的信息，请参阅 [**调谐器 \_ 模拟 \_ cap \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tuner_analog_caps_s) 结构。

*KsTvTune.ax* 将使用 "结算时间" 值作为近似值。 *KsTvTune.ax* 可以提供一个应用程序，该应用程序可以根据扫描频率范围和检测范围，对扫描进程可能会花费的时间进行密切估算。 调用驱动程序的 [**KSEVENT \_ 调谐器 \_ 启动 \_ 扫描**](./ksevent-tuner-initiate-scan.md) 事件以启动扫描进程后，应用程序可以等待事件通知规定时间。

对于硬件辅助扫描，根据调谐设备是否锁定到信号，驱动程序 \_ \_ 从对 \_ \_ 其 [**KSPROPERTY \_ 调谐器 \_ SCAN \_ status**](./ksproperty-tuner-scan-status.md) 属性的调用返回 "调谐器 LockType 无" 或 "调谐器 LockType 锁定" 状态。 如果驱动程序已锁定到信号，则驱动程序还会返回锁定信号的频率。

 


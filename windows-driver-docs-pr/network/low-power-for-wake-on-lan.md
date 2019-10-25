---
title: 在 LAN 上唤醒时离开低功耗状态
description: 在 LAN 上唤醒时离开低功耗状态
ms.assetid: 9ab8fa19-e75a-4266-accf-4e8b2964f82e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0610151f88b860fc002e441a1a97b847dcf3c3fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844138"
---
# <a name="low-power-for-wake-on-lan"></a>在 LAN 上唤醒时离开低功耗状态





LAN 唤醒（WOL）功能在网络适配器检测到 WOL 事件时从低功耗状态唤醒计算机。

小型端口驱动程序在初始化期间报告网络适配器 WOL 功能。 有关报告 WOL 功能的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

请注意，当计算机进入睡眠状态时，将取消媒体断开连接（D3 上的 D3）功能，以防止在外部切换链接状态时唤醒计算机;也就是说，开关关闭后打开。 有关在断开连接时出现的 D3 的详细信息，请参阅[低能耗媒体断开连接](low-power-on-media-disconnect.md)。

下图说明了将网络适配器设置为低功率状态时发生的事件的顺序。

![说明将 nic 设置为低功率状态的事件序列的关系图](images/d3onsleep.png)

当 NDIS 将网络适配器置于低功耗状态时，将发生以下序列：

1.  NDIS 使用[OID\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)启用 LAN 唤醒并禁用媒体连接唤醒。 \_在**WakeUpFlags**成员中清除启用的\_\_链接上的 NDIS PM\_唤醒\_。

2.  NDIS [\_PNP\_设置了 OID，以\_将](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)新电源状态（D3）的微型端口驱动程序通知给微型端口驱动程序。

3.  小型端口驱动程序可以使用 NDIS\_状态指示未知的媒体连接状态[ **\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状态指示。 **MediaConnectStateUnknown**值是在[**NDIS\_LINK\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构的**MediaConnectState**成员中设置的。 有关详细信息，请参阅[**NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)文档。

4.  NDIS 会将[**IRP\_MN\_wait\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)IRP 发送 PCI Express （PCIe）总线，以等待 WOL 事件。

5.  NDIS 将[**IRP\_MN\_集\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)IRP 发送到 D3 总线，以将总线设置为 D3 状态。

下图说明了在 WOL 事件完成后，为网络适配器恢复全部功能所发生的事件的顺序。

![说明 wol 事件后用于将 nic 完全恢复到 nic 的事件序列的关系图](images/d0onwol.png)

网络适配器唤醒计算机时，会发生以下序列：

1.  网络适配器通过在 PCIe 总线上或在 PCI 总线上的 PME\# 上断言唤醒\# 来唤醒系统。

2.  总线完成挂起的[**IRP\_MN\_WAIT\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)IRP。 IRP 从断电序列的最后一步等待完成。

3.  NDIS 通过[**IRP\_MN\_集\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)IRP 设置总线到完全电源（D0）。

4.  NDIS 通知微型端口驱动程序网络适配器处于完全供电状态（D0），其中 oid [\_PNP\_集\_电源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)。

5.  网络适配器使用[**ndis\_状态通知 ndis\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状态指示。 **MediaConnectStateConnected**值是在[**NDIS\_LINK\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构的**MediaConnectState**成员中设置的。

从 NDIS 6.30 开始，如果微型端口驱动程序支持[**NDIS\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示，则如果网络适配器唤醒系统，则必须发出此状态通知。 驱动程序在处理 oid\_PNP 集的 OID 集请求时发出此状态通知[\_集\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)实现到完全电源（D0）状态的转换。

有关详细信息，请参阅[NDIS 唤醒原因状态指示](ndis-wake-reason-status-indications.md)。

 

 






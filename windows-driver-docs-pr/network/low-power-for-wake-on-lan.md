---
title: 在 LAN 上唤醒时离开低功耗状态
description: 在 LAN 上唤醒时离开低功耗状态
ms.assetid: 9ab8fa19-e75a-4266-accf-4e8b2964f82e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39acf24d3f0994a5639079a277e2f37255e91304
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356236"
---
# <a name="low-power-for-wake-on-lan"></a>在 LAN 上唤醒时离开低功耗状态





唤醒 LAN (WOL) 功能的网络适配器检测到 WOL 事件时唤醒计算机从低功耗状态。

在初始化期间，微型端口驱动程序报告网络适配器的 WOL 功能。 有关报告 WOL 功能的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

请注意，媒体上的较低电源断开连接 (D3 上的断开连接) 时在计算机进入睡眠状态，以防止唤醒计算机时从外部循环的链接状态; 取消功能它是一个开关打开时关闭和打开。 详细了解 D3 断开连接时，请参阅[媒体断开连接的低开机](low-power-on-media-disconnect.md)。

下图说明了将网络适配器设置为低功耗状态会发生事件的序列。

![说明要将 nic 设置为低功耗状态的事件序列关系图](images/d3onsleep.png)

NDIS 置于低功耗状态的网络适配器，当按以下顺序：

1.  使用 NDIS [OID\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)唤醒媒体以启用 LAN 唤醒，并禁用连接。 NDIS\_PM\_唤醒\_ON\_链接\_更改\_中清除已启用**WakeUpFlags**成员。

2.  使用 NDIS [OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)通知新的电源状态 (D3) 的微型端口驱动程序。

3.  微型端口驱动程序可能指示未知的媒体连接状态使用[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状态指示。 **MediaConnectStateUnknown**中设置值**MediaConnectState**的成员[ **NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)结构。 有关详细信息，请参阅[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)文档。

4.  NDIS 发送 PCI Express (PCIe) 总线[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP 要等待的 WOL 事件。

5.  NDIS 发送 PCIe 总线[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) IRP 将总线 D3 状态设置为。

下图说明了出现 WOL 事件之后还原到的网络适配器的全部功能的事件序列。

![说明要还原到 nic wol 事件之后的全部功能的事件序列关系图](images/d0onwol.png)

网络适配器唤醒计算机时将发生以下序列：

1.  网络适配器中唤醒系统通过断言唤醒\#PCIe 总线或 PME 上\#PCI 总线上。

2.  总线完成挂起[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP。 IRP 正在等待从关机序列的最后一步完成。

3.  NDIS 具有设置到全功率 (D0) 总线[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) IRP。

4.  NDIS 会通过 OID 集请求的通知的网络适配器是全功率 (D0) 的微型端口驱动程序[OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)。

5.  网络适配器通知 NDIS 媒体连接具有事件[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状态指示。 **MediaConnectStateConnected**中设置值**MediaConnectState**的成员[ **NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)结构。

如果微型端口驱动程序支持从 NDIS 6.30 [ **NDIS\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示，它必须发出这如果网络适配器中唤醒系统的状态通知。 此状态通知时处理 OID 设置驱动程序问题的请求[OID\_PNP\_设置\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)全功率 (D0) 状态转换。

有关详细信息，请参阅[NDIS 唤醒原因状态指示](ndis-wake-reason-status-indications.md)。

 

 






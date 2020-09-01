---
title: 在 LAN 上唤醒时离开低功耗状态
description: 在 LAN 上唤醒时离开低功耗状态
ms.assetid: 9ab8fa19-e75a-4266-accf-4e8b2964f82e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c2997381d27219d777507b84ea55dedbe61a9a6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215606"
---
# <a name="low-power-for-wake-on-lan"></a>在 LAN 上唤醒时离开低功耗状态





LAN 唤醒 (WOL) 功能在网络适配器检测到 WOL 事件时从低功耗状态唤醒计算机。

小型端口驱动程序在初始化期间报告网络适配器 WOL 功能。 有关报告 WOL 功能的详细信息，请参阅 [报告电源管理功能](reporting-power-management-capabilities.md)。

请注意，当计算机进入睡眠状态时，媒体断开 (D3 上的电量越低) 功能会在计算机进入睡眠状态时取消，以便在外部切换链接状态时阻止唤醒计算机;也就是说，开关关闭后打开。 有关在断开连接时出现的 D3 的详细信息，请参阅 [低能耗媒体断开连接](low-power-on-media-disconnect.md)。

下图说明了将网络适配器设置为低功率状态时发生的事件的顺序。

![说明将 nic 设置为低功率状态的事件序列的关系图](images/d3onsleep.png)

当 NDIS 将网络适配器置于低功耗状态时，将发生以下序列：

1.  NDIS 使用 [OID \_ PM \_ 参数](./oid-pm-parameters.md) 启用 LAN 唤醒并禁用媒体连接唤醒。 \_ \_ \_ \_ \_ \_ 已在**WAKEUPFLAGS**成员中清除 "已启用 NDIS PM 唤醒链接更改"。

2.  NDIS 使用 [OID \_ PNP \_ 设置 \_ 电源](./oid-pnp-set-power.md) 将新电源状态 (D3) 的微型端口驱动程序通知。

3.  微型端口驱动程序可以使用 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 状态指示指示未知的媒体连接状态。 **MediaConnectStateUnknown**值是在[**NDIS \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构的**MediaConnectState**成员中设置的。 有关详细信息，请参阅 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 文档。

4.  NDIS 将 (PCIe) 总线发送到一个 [**IRP \_ MN \_ 等待 \_ 唤醒**](../kernel/irp-mn-wait-wake.md) IRP，以等待 WOL 事件。

5.  NDIS 将 [**IRP \_ MN \_ 集 \_ 电源**](../kernel/irp-mn-set-power.md) irp 发送到 PCIe 总线，以将总线设置为 D3 状态。

下图说明了在 WOL 事件完成后，为网络适配器恢复全部功能所发生的事件的顺序。

![说明 wol 事件后用于将 nic 完全恢复到 nic 的事件序列的关系图](images/d0onwol.png)

网络适配器唤醒计算机时，会发生以下序列：

1.  网络适配器通过在 \# PCI 总线上通过对 PCIe 总线或 PME 进行唤醒来唤醒系统 \# 。

2.  总线完成挂起的 [**IRP \_ MN \_ WAIT \_ 唤醒**](../kernel/irp-mn-wait-wake.md) IRP。 IRP 从断电序列的最后一步等待完成。

3.  NDIS 通过 [**IRP \_ MN \_ SET \_ power**](../kernel/irp-mn-set-power.md) IRP 将总线设置为完全电源 (D0) 。

4.  NDIS 通知微型端口驱动程序网络适配器处于完全供电状态 (D0) 并且 oid 设置了 [oid \_ PNP \_ 集 \_ 功能](./oid-pnp-set-power.md)的请求。

5.  网络适配器使用 [**ndis \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 状态指示向 ndis 通知一个 media connect 事件。 **MediaConnectStateConnected**值是在[**NDIS \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构的**MediaConnectState**成员中设置的。

从 NDIS 6.30 开始，如果微型端口驱动程序支持 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示，则如果网络适配器唤醒系统，则必须发出此状态通知。 驱动程序在处理 oid [ \_ PNP \_ 设置 \_ ](./oid-pnp-set-power.md) 的 oid 设置请求时发出此状态通知，以将转换为全功耗 (D0) 状态。

有关详细信息，请参阅 [NDIS 唤醒原因状态指示](ndis-wake-reason-status-indications.md)。

 


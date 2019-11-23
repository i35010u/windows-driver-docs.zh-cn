---
title: 介质断开连接时降低功耗
description: 介质断开连接时降低功耗
ms.assetid: 592f3835-47ec-443a-9ab5-e700fed2f7f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afabbff8ec4d34f2e5218c659c0fb2223e52532b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844136"
---
# <a name="low-power-on-media-disconnect"></a>介质断开连接时降低功耗





当媒体断开连接时，低功率开启的媒体断开连接（"在断开连接时，D3 上的 D3" 功能）可节省电源。 重新连接媒体后，网络适配器将恢复到完全电源状态（D0）。

在以下情况下，NDIS 使用 D3 on disconnect 功能：

-   网络适配器硬件必须能够在 media connect 上生成唤醒事件。

-   微型端口驱动程序必须在[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**MinLinkChangeWakeUp**成员中报告网络适配器的唤醒事件功能。

-   **MinLinkChangeWakeUp**的值必须对应于[**IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)IRP 报告的[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构的**DeviceWake**成员的值。

-   微型端口驱动程序必须注册为 NDIS 6.20 驱动程序或更高版本。

-   网络适配器必须是以太网 PCI 适配器。

-   唤醒事件功能必须由 **\*DeviceSleepOnDisconnect** standard INF file 关键字启用。

-   计算机已完全接通电源时，计算机芯片组必须能够正确地传播唤醒事件。 NDIS 通过查询 DEVPKEY\_PciDevice\_S0WakeupSupported PCI 属性来验证这一点。

请注意，仅当计算机完全处于工作状态（S0）时，"断开连接" 上的 D3 才可用。 当计算机进入睡眠状态时，此功能会被取消，以防在链接状态外部切换时唤醒计算机;也就是说，开关关闭后打开。 有关在计算机进入睡眠状态时设置低功耗状态的详细信息，请参阅[LAN 唤醒的低功率](low-power-for-wake-on-lan.md)。

小型端口驱动程序在初始化期间报告 D3 上的断开连接功能。 有关在断开连接功能上报告 D3 的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

**\*DeviceSleepOnDisconnect**标准 INF file 关键字指定设备是否已启用或禁用在断开连接时支持 D3。 有关此 INF 关键字的详细信息，请参阅[电源管理的标准化 INF 关键字](standardized-inf-keywords-for-power-management.md)。

在初始化期间，在 "断开连接时支持 D3" 的微型端口驱动程序必须报告可以支持通知操作系统媒体连接事件的功能的最低性能级别。 微型端口驱动程序在[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**MinLinkChangeWakeUp**成员中报告电源级别。 例如，微型端口驱动程序可以报告**NdisDeviceStateD3**。

下图说明了在发生媒体断开连接事件后，将网络适配器设置为低功耗状态的事件的顺序。

![说明在媒体断开连接事件之后将 nic 设置为低功率状态的事件序列的关系图](images/d3ondisconnect.png)

当适配器检测到媒体断开连接时，将发生以下序列：

1.  网络适配器硬件检测到媒体断开连接事件，并将该信息传递给微型端口驱动程序。

2.  微型端口驱动程序使用 Ndis\_状态通知 NDIS 的媒体断开连接事件， [ **\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状态指示。 [**Ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含[**ndis\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构。 MediaConnectStateDisconnected 值是在**NDIS\_LINK\_状态**结构的**MediaConnectState**成员中设置的。

3.  NDIS 使用[OID\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)来禁用 LAN 唤醒，并启用对媒体连接的唤醒连接（NDIS\_PM\_唤醒\_在\_链接上，在**WakeUpFlags**成员中设置\_\_更改。

4.  NDIS 使用[oid\_PNP\_集\_电源 OID 将](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)新电源状态（D3）的微型端口驱动程序通知给微型端口驱动程序。

5.  NDIS 向 PCIe 总线发送[**IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)IRP 等待重新连接事件。

6.  NDIS 通过[**IRP\_MN\_集\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)IRP 设置 PCIe 总线到 D3 状态。

下图说明了在 media connect 事件之后用于还原网络适配器的全部功能的事件的顺序。

![说明在媒体连接事件之后为 nic 恢复完全电源的事件序列的关系图](images/d0onconnect.png)

重新连接媒体时，将发生以下序列：

1.  网络适配器通过在 PCIe 总线上或在 PCI 总线上的 PME\# 上断言唤醒\# 来唤醒系统。

2.  总线完成挂起的[**IRP\_MN\_WAIT\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)IRP。 IRP 正在断开连接序列中的最后一步。

3.  NDIS 通过[**IRP\_MN\_集\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)IRP 设置总线到完全电源（D0）。

4.  NDIS 通知微型端口驱动程序网络适配器处于完全电源（D0）状态，并将 oid 设置为[oid\_PNP\_集\_电源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)。

5.  网络适配器使用[**ndis\_状态通知 ndis\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)状态指示。 **MediaConnectStateConnected**值是在[**NDIS\_LINK\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构的**MediaConnectState**成员中设置的。

从 NDIS 6.30 开始，如果微型端口驱动程序支持[**NDIS\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示，则如果网络适配器唤醒系统，则必须发出此状态通知。 驱动程序在处理 oid\_PNP 集的 OID 集请求时发出此状态通知[\_集\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)实现到完全电源（D0）状态的转换。

有关详细信息，请参阅[NDIS 唤醒原因状态指示](ndis-wake-reason-status-indications.md)。

**请注意**  如果微型端口驱动程序发出[**ndis\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状态指示，则必须在发出[**ndis\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)之前执行此操作，\_状态状态指示。\_

 

 

 






---
title: 介质断开连接时降低功耗
description: 介质断开连接时降低功耗
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b66e6821cbac9cff7213dcc6c4ab17c56e1037a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832219"
---
# <a name="low-power-on-media-disconnect"></a>介质断开连接时降低功耗





断开连接时，低功耗 (D3 上的 D3) 功能可通过将网络适配器置于低功耗状态， (D3) 在媒体断开连接时将其关闭。 重新连接媒体后，网络适配器将恢复到完全电源状态 (D0) 。

在以下情况下，NDIS 使用 D3 on disconnect 功能：

-   网络适配器硬件必须能够在 media connect 上生成唤醒事件。

-   微型端口驱动程序必须在 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的 **MinLinkChangeWakeUp** 成员中报告网络适配器的唤醒事件功能。

-   **MinLinkChangeWakeUp** 的值必须对应于 [**irp \_ MN \_ 查询 \_ 功能**](../kernel/irp-mn-query-capabilities.md)Irp 报告的 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构的 **DeviceWake** 成员值。

-   微型端口驱动程序必须注册为 NDIS 6.20 驱动程序或更高版本。

-   网络适配器必须是以太网 PCI 适配器。

-   唤醒事件功能必须通过 **\* DEVICESLEEPONDISCONNECT** standard INF file 关键字启用。

-   计算机已完全接通电源时，计算机芯片组必须能够正确地传播唤醒事件。 NDIS 通过查询 DEVPKEY \_ PciDevice S0WAKEUPSUPPORTED PCI 属性来验证这一点 \_ 。

请注意，"断开连接" 上的 D3 仅在计算机完全处于工作状态 (S0) 时可用。 当计算机进入睡眠状态时，此功能会被取消，以防在链接状态外部切换时唤醒计算机;也就是说，开关关闭后打开。 有关在计算机进入睡眠状态时设置低功耗状态的详细信息，请参阅 [LAN 唤醒的低功率](low-power-for-wake-on-lan.md)。

小型端口驱动程序在初始化期间报告 D3 上的断开连接功能。 有关在断开连接功能上报告 D3 的详细信息，请参阅 [报告电源管理功能](reporting-power-management-capabilities.md)。

**\* DEVICESLEEPONDISCONNECT** standard INF file 关键字指定设备是否已启用或禁用在断开连接时支持 D3。 有关此 INF 关键字的详细信息，请参阅 [电源管理的标准化 INF 关键字](standardized-inf-keywords-for-power-management.md)。

在初始化期间，在 "断开连接时支持 D3" 的微型端口驱动程序必须报告可以支持通知操作系统媒体连接事件的功能的最低性能级别。 微型端口驱动程序报告 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的 **MinLinkChangeWakeUp** 成员中的电源级别。 例如，微型端口驱动程序可以报告 **NdisDeviceStateD3**。

下图说明了在发生媒体断开连接事件后，将网络适配器设置为低功耗状态的事件的顺序。

![说明在媒体断开连接事件之后将 nic 设置为低功率状态的事件序列的关系图](images/d3ondisconnect.png)

当适配器检测到媒体断开连接时，将发生以下序列：

1.  网络适配器硬件检测到媒体断开连接事件，并将该信息传递给微型端口驱动程序。

2.  微型端口驱动程序使用 [**ndis \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 状态指示通知 ndis 的媒体断开连接事件。 [**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含 [**ndis \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构。 MediaConnectStateDisconnected 值是在 **NDIS \_ 链接 \_ 状态** 结构的 **MediaConnectState** 成员中设置的。

3.  NDIS 使用 [OID \_ pm \_ 参数](./oid-pm-parameters.md) 禁用 LAN 唤醒功能，启用对媒体连接的唤醒连接 (\_ \_ \_ \_ \_ \_ 在 **WakeUpFlags** 成员) 中设置启用的链接更改 "启用"。

4.  NDIS 使用 [oid \_ PNP \_ 集 \_ 电源](./oid-pnp-set-power.md) oid 将新电源状态 (D3) 的微型端口驱动程序通知给。

5.  NDIS 将 [**IRP \_ MN \_ 等待 \_ 唤醒**](../kernel/irp-mn-wait-wake.md) IRP 发送到 PCIe 总线，以等待重新连接事件。

6.  NDIS 通过 [**IRP \_ MN \_ SET \_ POWER**](../kernel/irp-mn-set-power.md) IRP 将 PCIe 总线设置为 D3 状态。

下图说明了在 media connect 事件之后用于还原网络适配器的全部功能的事件的顺序。

![说明在媒体连接事件之后为 nic 恢复完全电源的事件序列的关系图](images/d0onconnect.png)

重新连接媒体时，将发生以下序列：

1.  网络适配器通过在 \# PCI 总线上通过对 PCIe 总线或 PME 进行唤醒来唤醒系统 \# 。

2.  总线完成挂起的 [**IRP \_ MN \_ WAIT \_ 唤醒**](../kernel/irp-mn-wait-wake.md) IRP。 IRP 正在断开连接序列中的最后一步。

3.  NDIS 通过 [**IRP \_ MN \_ SET \_ power**](../kernel/irp-mn-set-power.md) IRP 将总线设置为完全电源 (D0) 。

4.  NDIS 通知微型端口驱动程序网络适配器处于完全电源 (D0) 状态，并且 oid 设置了 [oid \_ PNP \_ 集 \_ 功能](./oid-pnp-set-power.md)的请求。

5.  网络适配器使用 [**ndis \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 状态指示向 ndis 通知一个 media connect 事件。 **MediaConnectStateConnected** 值是在 [**NDIS \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构的 **MediaConnectState** 成员中设置的。

从 NDIS 6.30 开始，如果微型端口驱动程序支持 [**NDIS \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示，则如果网络适配器唤醒系统，则必须发出此状态通知。 驱动程序在处理 oid [ \_ PNP \_ 设置 \_ ](./oid-pnp-set-power.md) 的 oid 设置请求时发出此状态通知，以将转换为全功耗 (D0) 状态。

有关详细信息，请参阅 [NDIS 唤醒原因状态指示](overview-of-ndis-wake-reason-statue-indications.md)。

**注意**  如果微型端口驱动程序发出 [**ndis \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md) 状态指示，则必须在发出 [**ndis \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 状态指示之前执行此操作。

 

 


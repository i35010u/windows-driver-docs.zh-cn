---
title: 报告唤醒原因状态指示功能
description: 报告唤醒原因状态指示功能
ms.assetid: A72D04F7-EB09-4B1B-9AF5-7FEBC2514CE9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42accf8a97d710ba5eb3db13be6896ec8fb74a3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842037"
---
# <a name="reporting-wake-reason-status-indication-capabilities"></a>报告唤醒原因状态指示功能


从 NDIS 6.30 开始，微型端口驱动程序必须报告它是否可以发出 NDIS 唤醒原因状态指示（[**ndis\_状态\_PM\_唤醒\_原因**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)），以报告以下其中一项导致的唤醒事件:

-   网络适配器接收到与 LAN 唤醒（WOL）模式匹配的数据包。 这包括接收与通过对象标识符（OID）设置的 OID 指定的接收筛选器的数据包， [\_代\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)。

    **注意**  此类型的唤醒原因状态指示，网络适配器必须能够保存接收的数据包。 驱动程序必须在状态指示内返回接收的数据包。

     

-   网络适配器检测到特定于介质的事件，例如从802.11 接入点（AP）解除与移动宽带（MB）短消息服务（SMS）消息的接收。

-   网络适配器检测到另一个已启用的事件，该事件不特定于 WOL 模式或媒体类型（与*媒体无关的事件*）。 例如，如果启用网络适配器来检测媒体连接或断开连接，微型端口驱动程序会发出[ **\_PM\_唤醒\_原因状态指示的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)。

**注意**  支持 NDIS 唤醒原因状态指示对于移动宽带（MB）微型端口驱动程序是可选的。

 

当 NDIS 调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，微型端口驱动程序通过执行以下步骤来报告其唤醒原因状态指示功能：

1.  小型小型驱动程序使用基础硬件的电源管理功能初始化[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。

    若要启用对唤醒原因状态指示的支持，微型端口驱动程序必须将 NDIS 的成员设置[ **\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构，如下所示：

    -   微型端口驱动程序必须指定 NDIS\_PM\_功能\_修订版本\_2，NDIS\_SIZEOF [ **\_\_\_\_NDIS\_PM\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**标头**成员内的功能结构。
    -   如果网络适配器可以存储导致系统唤醒事件的接收数据包，则微型端口驱动程序会将 NDIS\_PM\_唤醒\_数据包\_\_指示此构造.

        如果设置了此标志，网络适配器必须能够保存收到的数据包，该数据包导致适配器生成唤醒事件。 此外，小型端口驱动程序必须能够在网络适配器转换为完全电源状态之后，在此数据包中执行以下操作：

        -   微型端口驱动程序必须能够通过调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)来指示数据包。

        -   微型端口驱动程序必须能够[ **\_PM\_唤醒\_原因状态指示发出 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)，并且必须通过指示传递数据包。

    -   微型端口驱动程序将**MaxWoLPacketSaveBuffer**成员设置为包含导致系统唤醒事件的 WOL 数据包的缓冲区的最大大小（以字节为单位）。

        **MaxWoLPacketSaveBuffer**成员的值必须小于或等于网络媒体的最大传输单元（MTU）和媒体访问控制（MAC）标头的大小（以字节为单位）。 驱动程序通过 oid 查询[\_GEN\_最大\_帧\_大小](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)的 oid 请求来报告 MTU 大小。

    -   微型端口驱动程序将**SupportedWakeUpEvents**设置为网络适配器所支持的与媒体无关的唤醒事件，例如当适配器连接到网络接口时生成唤醒事件。

    -   微型端口驱动程序将**MediaSpecificWakeUpEvents**设置为网络适配器所支持的特定于媒体的唤醒事件。 这些事件包括在802.11 适配器与 AP 解除关联时生成唤醒事件。

2.  微型端口驱动程序初始化[**ndis\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构，并将**PowerManagementCapabilitiesEx**成员设置为已初始化的[**NDIS\_PM 的地址\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。

3.  微型端口驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数以注册其电源管理功能。 当微型端口驱动程序调用此函数时，它会将*MiniportAttributes*参数设置为[**NDIS\_微型端口\_适配器的地址\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构。

微型端口驱动程序用来报告唤醒原因状态指示功能的方法基于用于报告电源管理功能的 NDIS 6.20 方法。 有关此方法的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

有关如何报告电源管理功能的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

 

 






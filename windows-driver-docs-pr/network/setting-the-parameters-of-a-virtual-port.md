---
title: 设置虚拟端口的参数
description: 设置虚拟端口的参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9837d9ad4a6d95abf64b7d7b601decce7699a399
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248284"
---
# <a name="setting-the-parameters-of-a-virtual-port"></a>设置虚拟端口的参数


覆盖驱动程序可以在支持单一根 i/o 虚拟化 (SR-IOV) 的网络适配器上的 NIC 交换机上更改虚拟端口 (VPort) 的参数。 驱动程序 (OID 发出对象标识符) 设置 [oid \_ NIC \_ SWITCH \_ VPORT \_ 参数](./oid-nic-switch-vport-parameters.md) 的请求以更改这些参数。

在过量驱动程序发出此 OID 集请求之前，必须使用要在 VPort 上更改的参数来初始化 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构。 然后，该驱动程序将为 OID 请求初始化 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) 结构，并将 **InformationBuffer** 成员设置为指向 **NDIS \_ NIC \_ SWITCH \_ VPORT \_ 参数** 结构的指针。

只能更改 VPort 的配置参数的有限子集。 过量驱动程序通过设置 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构的以下成员来指定要更改的参数：

-   **SwitchId** 成员必须设置为要为其返回参数的 NIC 交换机的标识符。

    **注意**  从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 " *默认 NIC 交换机*"。 **SwitchId** 成员必须设置为 NDIS \_ 默认 \_ 交换机 \_ ID。

     

-   **VPortId** 成员必须设置为与 VPort 关联的标识符。 过量驱动程序通过以下方式之一获取 VPort 标识符：

    -   从 Oid NIC 交换机的上一个 OID 方法请求 [ \_ \_ \_ 创建 \_ VPORT](./oid-nic-switch-create-vport.md)。

    -   从 [oid \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS](./oid-nic-switch-enum-vports.md)的上一个 oid 方法请求开始。

-   \_ \_ \_ 必须在 flags 成员中设置相应的 NDIS NIC 交换机 VPORT \_ PARAMS \_ *Xxx* \_ 更改的标志。 仅当在 Ntddndis 中定义了相应的 NDIS nic 开关 VPORT [**\_ \_ \_ \_**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) \_ \_ \_ \_ PARAMS \_ *Xxx* \_ changed 标志时，才能更改 NDIS nic 交换机 VPORT 参数结构的成员。

-   [**Ndis \_ nic \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的成员（该结构对应于 \_ \_ flags 成员中的 ndis nic 开关 \_ VPORT \_ PARAMS \_ *Xxx* \_ 更改标志集 ）是通过要更改的 VPORT 配置参数设置的。

从 Windows Server 2012 开始，只能通过 oid [ \_ nic \_ switch \_ VPORT \_ 参数](./oid-nic-switch-vport-parameters.md)的 Oid 集请求来更改以下 [**NDIS \_ nic \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的成员：

<a href="" id="portname"></a>**Portvalue**  
此成员包含 VPort 的用户友好说明。

<a href="" id="interruptmoderation"></a>**InterruptModeration**  
此成员指定 VPort 的中断裁决设置。

<a href="" id="processoraffinity"></a>**ProcessorAffinity**  
此成员指定可与此 VPort 相关联的 Cpu 的组号和位图。

过量驱动程序必须遵循以下准则来更改 VPort 的 **ProcessorAffinity** 成员：

-   此成员仅对附加到 PF 的 VPorts 有效。 此字段对于附加到 VF 的非默认 VPorts 无效。

-   对于附加到 PF 的非默认 VPorts，创建 VPort 时必须指定至少一个处理器。 创建 VPort 后，可以更改与非默认 VPort 关联的处理器关联。

    **注意**  非默认 VPorts 是通过 oid [ \_ NIC \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)的 oid 方法请求创建的。

     

<a href="" id="vportstate"></a>**VPortState**  
此成员指定 VPort 的当前状态。

过量驱动程序必须遵循以下准则来更改 VPort 的 **VPortState** 成员：

-   对于附加到 VF 的非默认 VPort， **VPortState** 成员必须始终设置为 **NdisNicSwitchVPortStateActivated**。

-   对于附加到 PF 的非默认 VPort，在创建 VPort 时，必须将 **VPortState** 成员设置为 **NdisNicSwitchVPortStateDeactivated** 。 仅当覆盖了 oid [ \_ NIC \_ 交换机 \_ VPort \_ 参数](./oid-nic-switch-vport-parameters.md) 由过量驱动程序发出以将 VPortState 更改为已激活状态之后，才会激活 PF VPort。

    激活非默认 VPort 时，PF 微型端口驱动程序可以为 VPort 分配资源，如通过 [**NdisAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)分配的共享内存。 激活 PF 微端口驱动程序后，在该驱动程序通过 oid [ \_ NIC \_ SWITCH \_ DELETE \_ VPort](./oid-nic-switch-delete-vport.md)的 oid 集请求删除 VPort 之前，可以随时为 VPort 分配资源。

-   默认 VPort 始终处于激活状态。 对于默认 VPort， **VPortState** 成员的值始终必须设置为 **NdisNicSwitchVPortStateActivated** 。

-   当 VPort 处于激活状态时，无法将其停用。 仅当 VPort 处于激活状态，并且在 VPort 上设置相应的 MAC 筛选器时，PF 微型端口驱动程序才能接收和传输来自该的数据包。 但是，在通过 oid [ \_ NIC \_ 交换机 \_ DELETE \_ VPort](./oid-nic-switch-delete-vport.md)的 oid 集请求删除 VPort 之后，驱动程序必须释放为 VPort 分配的资源。 驱动程序还必须在 VPort 上取消包的所有挂起的传输或接收操作。

当 PF 微型端口驱动程序接收 [oid \_ NIC \_ SWITCH \_ VPORT \_ 参数](./oid-nic-switch-vport-parameters.md)的 oid 集请求后，该驱动程序将用配置参数配置硬件。 此驱动程序只能在 \_ \_ \_ \_ \_  \_ [**ndis \_ nic \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的 **flags** 成员中更改由 ndis nic 交换机 VPORT 参数 Xxx 更改的标志。

 


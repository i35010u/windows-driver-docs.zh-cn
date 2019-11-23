---
title: 设置虚拟端口的参数
description: 设置虚拟端口的参数
ms.assetid: 92CBE5B2-897D-4B34-9AB9-8207C42A72BF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1caf3b48ace1d3db498f05d20a5a94df397fcc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841929"
---
# <a name="setting-the-parameters-of-a-virtual-port"></a>设置虚拟端口的参数


过量驱动程序可以在支持单一根 i/o 虚拟化（SR-IOV）的网络适配器上的 NIC 交换机上更改虚拟端口（VPort）的参数。 驱动程序发出 OID\_NIC 的对象标识符（OID）设置请求[\_SWITCH\_VPORT\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)更改这些参数。

在过量驱动程序发出此 OID 集请求之前，它必须使用 VPort 上要更改的参数来初始化[**NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。 然后，该驱动程序将为 OID 请求初始化[**NDIS\_oid\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构，并将**InformationBuffer**成员设置为指向**NDIS\_NIC\_SWITCH\_VPORT\_参数**结构的指针。

只能更改 VPort 的配置参数的有限子集。 过量驱动程序通过设置 NDIS\_NIC 的以下成员来指定要更改的参数[ **\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构：

-   **SwitchId**成员必须设置为要为其返回参数的 NIC 交换机的标识符。

    **注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 "*默认 NIC 交换机*"。 **SwitchId**成员必须设置为 NDIS\_默认\_交换机\_ID。

     

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 过量驱动程序通过以下方式之一获取 VPort 标识符：

    -   通过[oid\_NIC\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)的上一个 oid 方法请求\_CREATE\_VPORT。

    -   \_\_NIC 的上一个 OID 方法请求[\_枚举\_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)。

-   必须在**flags**成员中设置相应的 NDIS\_NIC\_交换机\_VPORT\_参数\_*XXX*\_的更改标志。 仅当在 Ntddndis 中定义了相应的 NDIS\_NIC\_\_\_\_\_ *\_* 参数时，NDIS\_nic 的成员才能更改[ **\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。

-   [**Ndis\_nic 的成员\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构，该结构对应于在**Flags**成员的 VPORT 配置参数设置的 NDIS\_NIC\_交换机\_VPORT\_*参数\_\_*

从 Windows Server 2012 开始，只能通过 oid [ **\_nic\_开关\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构中的以下成员进行更改参数结构\_[VPORT\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)：\_\_

<a href="" id="portname"></a>**Portvalue**  
此成员包含 VPort 的用户友好说明。

<a href="" id="interruptmoderation"></a>**InterruptModeration**  
此成员指定 VPort 的中断裁决设置。

<a href="" id="processoraffinity"></a>**ProcessorAffinity**  
此成员指定可与此 VPort 相关联的 Cpu 的组号和位图。

过量驱动程序必须遵循以下准则来更改 VPort 的**ProcessorAffinity**成员：

-   此成员仅对附加到 PF 的 VPorts 有效。 此字段对于附加到 VF 的非默认 VPorts 无效。

-   对于附加到 PF 的非默认 VPorts，创建 VPort 时必须指定至少一个处理器。 创建 VPort 后，可以更改与非默认 VPort 关联的处理器关联。

    **请注意**  非默认 VPorts 是通过 OID\_NIC 的 oid 方法请求创建的[\_交换机\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。

     

<a href="" id="vportstate"></a>**VPortState**  
此成员指定 VPort 的当前状态。

过量驱动程序必须遵循以下准则来更改 VPort 的**VPortState**成员：

-   对于附加到 VF 的非默认 VPort， **VPortState**成员必须始终设置为**NdisNicSwitchVPortStateActivated**。

-   对于附加到 PF 的非默认 VPort，在创建 VPort 时，必须将**VPortState**成员设置为**NdisNicSwitchVPortStateDeactivated** 。 仅当 oid [\_NIC\_交换机\_VPort\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)由过量驱动程序发出以将 VPortState 更改为已激活状态之后，才会激活 PF VPort。

    激活非默认 VPort 时，PF 微型端口驱动程序可以为 VPort 分配资源，如通过[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)分配的共享内存。 激活 PF 微端口驱动程序后，在该驱动程序通过 oid [\_NIC\_开关\_DELETE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)删除该 VPort 时，可以随时为 VPort 分配资源。

-   默认 VPort 始终处于激活状态。 对于默认 VPort， **VPortState**成员的值始终必须设置为**NdisNicSwitchVPortStateActivated** 。

-   当 VPort 处于激活状态时，无法将其停用。 仅当 VPort 处于激活状态，并且在 VPort 上设置相应的 MAC 筛选器时，PF 微型端口驱动程序才能接收和传输来自该的数据包。 但是，在通过 oid [\_NIC\_交换机\_DELETE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)删除 VPort 之后，驱动程序必须释放为 VPort 分配的资源。 驱动程序还必须在 VPort 上取消包的所有挂起的传输或接收操作。

在 PF 微型端口驱动程序接收[oid\_NIC\_开关\_VPORT\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)后，该驱动程序将用配置参数配置硬件。 该驱动程序只能更改由 NDIS\_NIC 标识的配置参数，\_交换机\_VPORT\_参数\_*Xxx*\_\_\_\_ [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)

 

 






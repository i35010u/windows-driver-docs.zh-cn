---
title: 基于虚拟端口的数据包流
description: 基于虚拟端口的数据包流
ms.assetid: 1E4B1987-3288-4082-B8A8-0F275C61597F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9119c8a97dd4203612d211d2674ff91bcfb55fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363781"
---
# <a name="packet-flow-over-a-virtual-port"></a>基于虚拟端口的数据包流


默认 NIC 切换为支持单个根 I/O 虚拟化 (SR-IOV) 接口的网络适配器的一个组件。 该开关始终将默认虚拟端口 (VPort) 附加到 PCI Express (PCIe) 物理函数 (PF)。 此开关可以将一个或多个非默认 VPorts 附加到 PF. 有关详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

以下几点适用于发送或附加到 PF VPort 上接收的数据包：

-   数据包通过发送或接收 VPort VPort 标识符值为指定的默认**默认\_VPORT\_ID**。

    数据包通过发送或接收 VPorts 用 VPort 创建通过 OID 方法的请求时返回的 VPort 标识符指定的非默认[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。 当驱动程序处理此 OID 请求时，它获取从 VPort 标识符**VPortId**的成员[ **NDIS\_NIC\_开关\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)与 OID 请求关联的结构。

    **请注意**  时 VPort 删除，则可以为微型端口驱动程序以接收包含一个无效的 NBL **VPortId**值。 如果发生这种情况，微型端口应忽略 VPort ID 无效，并使用**默认\_VPORT\_ID**相反。 **VPortId**中找到**NetBufferListFilteringInfo** NBL 部分的 OOB 数据，并通过使用检索[ **NET\_缓冲区\_列表\_接收\_筛选器\_VPORT\_ID** ](https://msdn.microsoft.com/library/windows/hardware/hh439946)宏。

     

-   PF 微型端口驱动程序调用[ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)以指示从 VPort 接收的数据包。 PF 微型端口驱动程序调用之前**NdisMIndicateReceiveNetBufferLists**，它必须在中的带外 (OOB) 数据中设置 VPort 标识符[ **NET\_缓冲区\_列表** ](https://msdn.microsoft.com/library/windows/hardware/ff568388)数据包的结构。 该驱动程序通过使用实现这[ **NET\_缓冲区\_列表\_接收\_筛选器\_VPORT\_ID** ](https://msdn.microsoft.com/library/windows/hardware/hh439946)宏。

-   虚拟化堆栈调用[ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)传输到 VPort 的数据包。 虚拟化堆栈调用之前**NdisSendNetBufferLists**，它的 OOB 数据中设置的 VPort 标识符[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)数据包的结构。

    微型端口驱动程序使用获取 VPort 标识符[ **NET\_缓冲区\_列表\_接收\_筛选器\_VPORT\_ID**](https://msdn.microsoft.com/library/windows/hardware/hh439946)宏。

    微型端口驱动程序必须队列上指定 VPort 的硬件传输队列传输数据包。

**请注意**  PCIe 虚拟函数 (VF) 有关的微型端口驱动程序不会设置或查询的 OOB 数据中的 VPort 标识符[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)数据包的结构。 当 VF 微型端口驱动程序发送数据包时，它队列上附加到 VF VPort 单一的非默认的硬件传输队列数据包。

 

 

 






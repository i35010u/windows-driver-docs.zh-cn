---
title: 为虚拟功能分配资源
description: 为虚拟功能分配资源
ms.assetid: 00191D2C-E093-4DB7-AC82-8E8E5A74656F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2716e636670a0593e9a602d8d1226d2862938844
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835298"
---
# <a name="allocating-resources-for-a-virtual-function"></a>为虚拟功能分配资源


支持单根 i/o 虚拟化（SR-IOV）的网络适配器必须能够支持下列硬件组件：

-   一个 PCI Express （PCIe）物理函数（PF）。 PF 始终存在于网络适配器上，并附加到 Hyper-v 父分区。

    有关此硬件组件的详细信息，请参阅[Sr-iov 物理函数（PF）](sr-iov-physical-function--pf-.md)。

-   一个或多个 PCIe 虚函数（VF）。 必须将每个 VF 初始化并附加到 Hyper-v 子分区，来宾操作系统的网络组件才能通过 VF 发送或接收数据包。

    有关此硬件组件的详细信息，请参阅[Sr-iov 虚拟函数（VFs）](sr-iov-virtual-functions--vfs-.md)。

PF 微型端口驱动程序（在 Hyper-v 父分区的管理操作系统中运行）为 PF 和 SR-IOV 网络适配器上的每个 VF 分配资源。 此驱动程序为 PF 分配资源，就像对任何网络适配器一样。 但是，驱动程序将按以下方式为每个 VF 分配资源：

-   当驱动程序在网络适配器上创建网络接口卡（NIC）时，PF 微型端口驱动程序为每个 VF 分配硬件资源。 驱动程序通过调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)来完成 VFs 的硬件资源分配。 有关此过程的详细信息，请参阅[创建 NIC 交换机](creating-a-nic-switch.md)。

-   当驱动程序处理 OID 的对象标识符（OID）方法请求时，PF 微型端口驱动程序会为 VF 分配软件资源[\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 即使已为 VF 分配硬件资源，也会将其视为 nonoperational，直到 PF 微端口驱动程序成功完成 OID\_NIC\_交换机\_分配\_VF。

过量驱动程序可以通过\_\_NIC 发出 oid 方法请求为 VF 请求分配软件资源， [\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 \_oid 的[**ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_NIC 的指针\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。

成功从 OID 请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)构造. 此结构具有适配器唯一的 VF 标识符和 PCI 请求程序标识符（RID）。 这些标识符通过以下方式使用：

-   过量驱动程序在与 VF 相关的操作中使用 VF 标识符，如下所示：

    -   通过 oid 的 oid 方法请求获取当前的 VF 参数[\_NIC\_SWITCH\_VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)。

    -   为 VF 释放以前分配的资源，通过 oid\_NIC 的 oid 集请求[\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)。

    -   通过 OID [\_SRIOV\_reset\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)的 oid 集请求向 VF 发出 PCI 重置。

-   虚拟化堆栈使用 RID 来重新映射 PF 和 VF 之间的 DMA 和中断。 RID 还允许硬件输入/输出内存管理单元（IOMMU）将来宾物理地址转换为主机物理地址。

有关过量驱动程序如何[\_\_nic 发出 oid 的详细信息\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)方法请求的详细信息，请参阅的[网络\_交换机颁发 oid\_分配\_VF 请求](issuing-oid-nic-switch-allocate-vf-requests.md)。

有关 PF 微型端口驱动程序如何处理[OID\_NIC 的详细信息\_交换机\_分配\_vf](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)方法请求的详细信息，请参阅[处理 oid\_NIC\_SWITCH\_分配\_VF 请求](handling-oid-nic-switch-allocate-vf-requests.md)。

**请注意**，在已通过 OID 的 oid 方法请求为某个 vf  分配了资源后[\_NIC\_SWITCH\_分配\_vf](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)，则不能动态更改 vf 的资源参数。

 

 

 






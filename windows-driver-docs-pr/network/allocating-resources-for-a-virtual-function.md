---
title: 为虚拟功能分配资源
description: 为虚拟功能分配资源
ms.assetid: 00191D2C-E093-4DB7-AC82-8E8E5A74656F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdc15c3671cd556185a993614326f31d76e12277
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206509"
---
# <a name="allocating-resources-for-a-virtual-function"></a>为虚拟功能分配资源


支持 (SR-IOV) 的单个根 i/o 虚拟化的网络适配器必须能够支持以下硬件组件：

-   一个 PCI Express (PCIe) 物理功能 (PF) 。 PF 始终存在于网络适配器上，并附加到 Hyper-v 父分区。

    有关此硬件组件的详细信息，请参阅 [Sr-iov 物理 Function (PF) ](sr-iov-physical-function--pf-.md)。

-   一个或多个 PCIe 虚拟功能 (VF) 。 必须将每个 VF 初始化并附加到 Hyper-v 子分区，来宾操作系统的网络组件才能通过 VF 发送或接收数据包。

    有关此硬件组件的详细信息，请参阅 [sr-iov)  (Sr-iov 虚拟函数 ](sr-iov-virtual-functions--vfs-.md)。

PF 微型端口驱动程序（在 Hyper-v 父分区的管理操作系统中运行）为 PF 和 SR-IOV 网络适配器上的每个 VF 分配资源。 此驱动程序为 PF 分配资源，就像对任何网络适配器一样。 但是，驱动程序将按以下方式为每个 VF 分配资源：

-   当驱动程序在网络适配器上创建网络接口卡 (NIC) 时，PF 微型端口驱动程序为每个 VF 分配硬件资源。 驱动程序通过调用 [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)来完成 VFs 的硬件资源分配。 有关此过程的详细信息，请参阅 [创建 NIC 交换机](creating-a-nic-switch.md)。

-   当驱动程序处理 [oid \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的对象标识符 (OID) 方法请求时，PF 微型端口驱动程序为 VF 分配软件资源。 即使已为 VF 分配硬件资源，也会将其视为 nonoperational，直到 PF 微端口驱动程序成功完成 OID \_ NIC \_ 交换机 \_ 分配 \_ VF。

过量驱动程序可以通过发出 [oid \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的 oid 方法请求，为 VF 请求分配软件资源。 OID 请求的[**ndis \_ oid \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的指针。

成功从 OID 请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的指针。 此结构具有适配器唯一的 VF 标识符和 PCI 请求者标识符 (RID) 。 这些标识符通过以下方式使用：

-   过量驱动程序在与 VF 相关的操作中使用 VF 标识符，如下所示：

    -   通过 oid [ \_ NIC \_ 开关 \_ VF \_ 参数](./oid-nic-switch-vf-parameters.md)的 OID 方法请求获取当前的 VF 参数。

    -   通过 oid [ \_ NIC \_ 交换机 \_ 自由 \_ VF](./oid-nic-switch-free-vf.md)的 oid 设置请求，释放以前分配给 VF 的资源。

    -   通过 oid [ \_ SRIOV \_ RESET \_ vf](./oid-sriov-reset-vf.md)的 oid 集请求向 vf 发出 PCI 重置。

-   虚拟化堆栈使用 RID 来重新映射 PF 和 VF 之间的 DMA 和中断。 RID 还允许硬件输入/输出内存管理单元 (IOMMU) 将来宾物理地址转换为主机物理地址。

有关过量驱动程序如何发出 [oid \_ nic \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md) 方法请求的详细信息，请参阅 [颁发 oid \_ nic \_ 交换机 \_ 分配 \_ vf 请求](issuing-oid-nic-switch-allocate-vf-requests.md)。

有关 PF 微型端口驱动程序如何处理 [oid \_ nic \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md) 方法请求的详细信息，请参阅 [处理 oid \_ nic \_ 交换机 \_ 分配 \_ vf 请求](handling-oid-nic-switch-allocate-vf-requests.md)。

**注意**   通过 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md)的 OID 方法请求分配了用于 vf 的资源后，无法动态更改 vf 的资源参数。

 

 


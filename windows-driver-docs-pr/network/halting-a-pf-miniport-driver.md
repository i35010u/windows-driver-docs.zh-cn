---
title: 停止 PF 微型端口驱动程序
description: 停止 PF 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19954d7c931dbf27fd65d9a7dc6bb319122b0fcf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840021"
---
# <a name="halting-a-pf-miniport-driver"></a>停止 PF 微型端口驱动程序


本主题讨论在支持单根 i/o 虚拟化 (SR-IOV) 的适配器上，为 PCI Express (PCIe) 物理功能 (PF) 停止微型端口驱动程序所涉及的步骤。 下图显示了这些步骤。

![完整文本中所述过程的图像，其中的请求和函数在过量驱动程序、ndis 和 pf 微型端口驱动程序之间流动。](images/sriov-pf-halt.png)

本主题包含以下信息：

-   [在调用 *MiniportHaltEx* 之前由 NDIS 和过量驱动程序执行的操作](#actions-performed-by-ndis-and-overlying-drivers-before-miniporthaltex-is-called)

-   [调用 *MiniportHaltEx* 时，PF 微型端口驱动程序执行的操作](#actions-performed-by-the-pf-miniport-driver-when-miniporthaltex-is-called)

## <a name="actions-performed-by-ndis-and-overlying-drivers-before-miniporthaltex-is-called"></a>在调用 *MiniportHaltEx* 之前由 NDIS 和过量驱动程序执行的操作


在 NDIS 调用 PF 微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数之前，先执行以下操作：

-   NDIS 取消绑定以前绑定到基础 PF 微型端口驱动程序的所有协议驱动程序。 NDIS 通过调用协议驱动程序的 [*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex) 函数来实现此功能。

-   NDIS 将以前绑定到基础 PF 微型端口驱动程序的所有筛选器驱动程序分离。 NDIS 通过调用筛选器驱动程序的 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数来实现此功能。

当过量协议或筛选器驱动程序未绑定或从 PF 微型端口驱动程序分离时，必须执行以下步骤：

1.  驱动程序必须 (OID 发出对象标识符) 设置 [oid 接收筛选器的请求 \_ \_ \_ 清除 \_ 筛选器](./oid-receive-filter-clear-filter.md) 以清除之前设置的任何接收筛选器。 驱动程序在默认虚拟端口 (VPort) 或网络适配器上 NIC 交换机的任何非默认 VPorts 上设置这些筛选器。 驱动程序设置这些筛选器的方法是：向 "PF" 微型端口驱动程序发出 [oid "oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md) 器" 请求。

2.  驱动程序必须发出 oid [ \_ nic \_ switch \_ delete \_ VPORT](./oid-nic-switch-delete-vport.md) 的 oid 集请求，才能删除先前在 NIC 交换机上创建的任何非默认的 VPorts。 驱动程序通过向 PF 微型端口驱动程序发出 [oid \_ NIC \_ SWITCH \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md) 的 Oid 方法请求来设置这些 VPorts。

3.  驱动程序必须发出 oid [ \_ nic \_ 交换机 \_ 自由 \_ VF](./oid-nic-switch-free-vf.md) 的 oid 集请求，以释放其之前在 NIC 交换机上分配的任何 PCIe 虚拟功能)  (的资源。 驱动程序为 VF 分配资源，方法是发出 Oid NIC 交换机的 OID 方法请求，将 [ \_ \_ \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md) 发送到 PF 微型端口驱动程序。

    有关详细信息，请参阅 [释放虚拟函数资源](freeing-resources-for-a-virtual-function.md)。

    **注意**  当释放 VF 的资源时，NDIS 会调用 VF 微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数。 有关详细信息，请参阅 [停止 VF 微型端口驱动程序](halting-a-vf-miniport-driver.md)。

     

在从 NIC 交换机中删除所有接收筛选器、非默认 VPorts 和 VFs 后，NDIS 执行以下步骤：

-   NDIS 通过颁发 oid [ \_ nic \_ 交换机 \_ 删除 \_ 交换机](./oid-nic-switch-delete-switch.md) 到 PF 微型端口驱动程序的 OID 集请求，删除所有 NIC 交换机。 有关如何删除 NIC 交换机的详细信息，请参阅 [删除 Nic 交换机](deleting-a-nic-switch.md)。

    **注意**  从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的默认 NIC 交换机。

     

-   成功删除所有 NIC 交换机后，NDIS 将调用 PF 微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数。

## <a name="actions-performed-by-the-pf-miniport-driver-when-miniporthaltex-is-called"></a>调用 *MiniportHaltEx* 时，PF 微型端口驱动程序执行的操作


当 NDIS 调用 *MiniportHaltEx* 时，PF 微型端口驱动程序必须执行以下步骤：

1.  如果 PF 微型端口驱动程序支持静态创建 NIC 交换机，并且已删除所有 NIC 交换机，则驱动程序必须通过调用 [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) ，并将 *EnableVirtualization* 参数设置为 FALSE，并将 *NumVFs* 参数设置为零，来禁用适配器上的虚拟化。

    [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) 清除 **NumVFs** 成员，并且 VF 在网络适配器的 PF 的 PCIe 配置空间中的 sr-iov 扩展功能结构中 **启用** 位。

    **注意** 如果 PF 微型端口驱动程序支持动态创建和配置 NIC 交换机，则当驱动程序处理 [oid \_ NIC \_ 交换机 \_ 删除 \_ 开关](./oid-nic-switch-delete-switch.md)的 oid 集请求时，它必须调用 [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) 。 此 OID 请求在调用 *MiniportHaltEx* 之前发出。

     

2.  PF 微型端口驱动程序执行与微型端口暂停操作关联的其他任务。 有关详细信息，请参阅 [停止微型端口适配器](halting-a-miniport-adapter.md)。

 


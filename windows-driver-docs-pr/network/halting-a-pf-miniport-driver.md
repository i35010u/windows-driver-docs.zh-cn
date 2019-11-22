---
title: 停止 PF 微型端口驱动程序
description: 停止 PF 微型端口驱动程序
ms.assetid: E3F6B78E-6938-459B-883E-5DA0BB1D73C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a85bd4d2b1de1ff1091a23f8f6259540ad7c953
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840481"
---
# <a name="halting-a-pf-miniport-driver"></a>停止 PF 微型端口驱动程序


本主题讨论在支持单根 i/o 虚拟化（SR-IOV）的适配器上停止 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序所涉及的步骤。 下图显示了这些步骤。

![完整文本中所述过程的图像，其中的请求和函数在过量驱动程序、ndis 和 pf 微型端口驱动程序之间流动。](images/sriov-pf-halt.png)

本主题包含下列信息：

-   [在调用*MiniportHaltEx*之前由 NDIS 和过量驱动程序执行的操作](#actions-performed-by-ndis-and-overlying-drivers-before-miniporthaltex-is-called)

-   [调用*MiniportHaltEx*时，PF 微型端口驱动程序执行的操作](#actions-performed-by-the-pf-miniport-driver-when-miniporthaltex-is-called)

## <a name="actions-performed-by-ndis-and-overlying-drivers-before-miniporthaltex-is-called"></a>在调用*MiniportHaltEx*之前由 NDIS 和过量驱动程序执行的操作


在 NDIS 调用 PF 微型端口驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数之前，先执行以下操作：

-   NDIS 取消绑定以前绑定到基础 PF 微型端口驱动程序的所有协议驱动程序。 NDIS 通过调用协议驱动程序的[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数来实现此功能。

-   NDIS 将以前绑定到基础 PF 微型端口驱动程序的所有筛选器驱动程序分离。 NDIS 通过调用筛选器驱动程序的[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)函数来实现此功能。

当过量协议或筛选器驱动程序未绑定或从 PF 微型端口驱动程序分离时，必须执行以下步骤：

1.  驱动程序必须发出[OID\_接收\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)的对象标识符（oid）设置请求，\_清除\_筛选器以清除之前设置的任何接收筛选器。 驱动程序在默认虚拟端口（VPort）或网络适配器上的 NIC 交换机的任何非默认 VPorts 上设置这些筛选器。 驱动程序设置这些筛选器的方法是：\_筛选器发出 oid 方法\_请求， [\_将\_筛选器设置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)为 PF 微型端口驱动程序。

2.  驱动程序必须发出 oid\_NIC 的 OID 集请求[\_交换机\_delete\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)删除先前在 NIC 交换机上创建的所有非默认的 VPorts。 驱动程序通过[\_\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)发出 oid 方法请求，\_创建到 PF 微型端口驱动程序的\_VPORT，来设置这些 VPorts。

3.  驱动程序必须发出 oid\_NIC 的 OID 集请求[\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放先前在 NIC 交换机上分配的任何 PCIe 虚拟功能（VFs）的资源。 驱动程序为 VF 分配资源，方法是[\_开关\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)发出 oid 方法请求，\_将\_VF 分配到 PF 微型端口驱动程序。

    有关详细信息，请参阅[释放虚拟函数资源](freeing-resources-for-a-virtual-function.md)。

    **请注意**  释放 vf 的资源时，NDIS 会调用 vf 微型端口驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数。 有关详细信息，请参阅[停止 VF 微型端口驱动程序](halting-a-vf-miniport-driver.md)。

     

在从 NIC 交换机中删除所有接收筛选器、非默认 VPorts 和 VFs 后，NDIS 执行以下步骤：

-   NDIS 通过发出 oid\_NIC 的 OID 集请求来删除所有 NIC 交换机[\_交换机\_DELETE\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)到 PF 微型端口驱动程序。 有关如何删除 NIC 交换机的详细信息，请参阅[删除 Nic 交换机](deleting-a-nic-switch.md)。

    **注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的默认 NIC 交换机。

     

-   成功删除所有 NIC 交换机后，NDIS 将调用 PF 微型端口驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数。

## <a name="actions-performed-by-the-pf-miniport-driver-when-miniporthaltex-is-called"></a>调用*MiniportHaltEx*时，PF 微型端口驱动程序执行的操作


当 NDIS 调用*MiniportHaltEx*时，PF 微型端口驱动程序必须执行以下步骤：

1.  如果 PF 微型端口驱动程序支持静态创建 NIC 交换机，且已删除所有 NIC 交换机，则驱动程序必须通过使用*EnableVirtualization*调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)来禁用适配器上的虚拟化。参数设置为 FALSE，并将*NumVFs*参数设置为零。

    [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)清除**NumVFs**成员，并且 VF 在网络适配器的 PF 的 PCIe 配置空间中的 sr-iov 扩展功能结构中**启用**位。

    **请注意**  如果 PF 微型端口驱动程序支持动态创建和配置 NIC 交换机，则当驱动程序处理 OID 的 oid 集请求时，它必须调用[**NDISMENABLEVIRTUALIZATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) ， [\_NIC\_开关\_DELETE\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)。 此 OID 请求在调用*MiniportHaltEx*之前发出。

     

2.  PF 微型端口驱动程序执行与微型端口暂停操作关联的其他任务。 有关详细信息，请参阅[停止微型端口适配器](halting-a-miniport-adapter.md)。

 

 






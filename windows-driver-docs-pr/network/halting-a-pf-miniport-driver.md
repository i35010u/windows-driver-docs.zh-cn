---
title: 停止 PF 微型端口驱动程序
description: 停止 PF 微型端口驱动程序
ms.assetid: E3F6B78E-6938-459B-883E-5DA0BB1D73C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bad3dd9360a8edf37da1bd5199205c69ecb0eb4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379839"
---
# <a name="halting-a-pf-miniport-driver"></a>停止 PF 微型端口驱动程序


本主题讨论与停止的 PCI Express (PCIe) 物理函数 (PF) 上支持单根 I/O 虚拟化 (SR-IOV) 的适配器的微型端口驱动程序所涉及的步骤。 下图中显示这些步骤。

![在基础驱动程序、 ndis 和 pf 微型端口驱动程序之间的请求和函数的流中的完整文本中所述的过程的图像。](images/sriov-pf-halt.png)

本主题包含下列信息：

-   [NDIS 和过量驱动程序之前的操作执行*MiniportHaltEx*称为](#actions-performed-by-ndis-and-overlying-drivers-before-miniporthaltex-is-called)

-   [通过 PF 微型端口驱动程序时的操作执行*MiniportHaltEx*称为](#actions-performed-by-the-pf-miniport-driver-when-miniporthaltex-is-called)

## <a name="actions-performed-by-ndis-and-overlying-drivers-before-miniporthaltex-is-called"></a>NDIS 和过量驱动程序之前的操作执行*MiniportHaltEx*称为


NDIS 调用 PF 微型端口驱动程序的前[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数，它首先执行以下操作：

-   NDIS 取消绑定以前绑定到基础 PF 微型端口驱动程序的所有协议驱动程序。 NDIS 将这是通过调用协议驱动程序[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)函数。

-   NDIS 分离具有以前绑定到基础 PF 微型端口驱动程序的所有筛选器驱动程序。 NDIS 将这是通过调用筛选器驱动程序[ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)函数。

当基础协议或筛选器驱动程序正在之间的绑定或 PF 微型端口驱动程序中分离出来，必须执行以下步骤：

1.  该驱动程序必须发出的对象标识符 (OID) 组请求[OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)可以清除任何以前设置的接收筛选器。 驱动程序的默认虚拟端口 (VPort) 或任何非默认的网络适配器上的 NIC 开关 VPorts 上设置这些筛选器。 驱动程序通过发出的 OID 方法请求设置这些筛选器[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)到 PF 微型端口驱动程序。

2.  该驱动程序必须发出的 OID 集请求[OID\_NIC\_切换\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)删除任何非默认 VPorts 之前创建的 NIC 开关。 驱动程序通过发出的 OID 方法请求设置这些 VPorts [OID\_NIC\_交换机\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)到 PF 微型端口驱动程序。

3.  该驱动程序必须发出的 OID 集请求[OID\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)释放它以前的 NIC 上分配任何 PCIe 虚函数 (VFs) 的资源切换。 该驱动程序分配资源的取景器发出的 OID 方法请求[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)到 PF 微型端口驱动程序。

    有关详细信息，请参阅[为虚拟函数释放资源](freeing-resources-for-a-virtual-function.md)。

    **请注意**  NDIS VF 的资源已释放，当调用[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt) VF 微型端口驱动程序的函数。 有关详细信息，请参阅[停止 VF 微型端口驱动程序](halting-a-vf-miniport-driver.md)。

     

所有接收非 VPorts，默认的筛选器，并已从删除 VFs 后 NIC 切换、 NDIS 按照以下步骤：

-   NDIS 通过发出的 OID 集请求中删除所有 NIC 开关[OID\_NIC\_交换机\_删除\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)到 PF 微型端口驱动程序。 有关如何删除 NIC 开关的详细信息，请参阅[删除 NIC 切换](deleting-a-nic-switch.md)。

    **请注意**  从 Windows Server 2012 开始，SR-IOV 接口仅支持的默认 NIC 切换上的网络适配器。

     

-   已成功删除所有 NIC 开关后，调用 NDIS [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt) PF 微型端口驱动程序的函数。

## <a name="actions-performed-by-the-pf-miniport-driver-when-miniporthaltex-is-called"></a>通过 PF 微型端口驱动程序时的操作执行*MiniportHaltEx*称为


当调用 NDIS *MiniportHaltEx*，PF 微型端口驱动程序必须执行以下步骤：

1.  如果 PF 微型端口驱动程序支持静态创建 NIC 的开关和所有已删除的 NIC 开关，该驱动程序必须通过调用禁用在适配器上的虚拟化[ **NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)与*EnableVirtualization*参数设置为 FALSE 并且*NumVFs*参数设置为零。

    [**NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)清除**NumVFs**成员并**VF 启用**位的 SR-IOV 扩展功能结构中的 PCIe 配置空间网络适配器的 PF.

    **请注意**  PF 微型端口驱动程序支持动态创建和配置的 NIC 开关，如果它必须调用[ **NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)时驱动程序处理OID 设置的请求[OID\_NIC\_交换机\_删除\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)。 此 OID 请求发出前*MiniportHaltEx*调用。

     

2.  PF 微型端口驱动程序执行与微型端口 halt 操作相关联的其他任务。 有关详细信息，请参阅[停止微型端口适配器](halting-a-miniport-adapter.md)。

 

 






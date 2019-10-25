---
title: NIC 交换机的静态创建
description: NIC 交换机的静态创建
ms.assetid: F325B1F8-7655-4044-AF04-32B434574082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d420205bb40d87e2a6f2d109af53efe651c05f98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841828"
---
# <a name="static-creation-of-a-nic-switch"></a>NIC 交换机的静态创建


支持单根 i/o 虚拟化（SR-IOV）的网络适配器必须能够创建 NIC 交换机。 对于某些适配器，可以在对[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用的上下文中以静态方式创建 NIC 开关。

只有 SR-IOV 适配器的 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序可以在适配器上创建 NIC 交换机。

**注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为*默认 NIC 交换机*，由 NDIS\_默认\_交换机\_ID 标识符引用。

 

默认 NIC 交换机的参数是在注册表中通过标准化关键字设置定义的。 有关这些关键字的详细信息，请参阅[sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

当 NDIS 调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，PF 微型端口驱动程序将静态创建 NIC 开关。 通常，驱动程序会先将 NIC 交换机作为其初始化序列的一部分进行创建和配置，然后才能在网络适配器上启用 SR-IOV。

在调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的上下文中，PF 微型端口驱动程序会按照以下步骤进行操作：静态创建 NIC 交换机，并在网络适配器上启用 sr-iov：

1.  PF 微型端口驱动程序必须读取 SR-IOV 标准化关键字，以确定是否已启用 SR-IOV 并获取 NIC 交换机配置参数。

    **请注意**  如果 PF 微型端口驱动程序已将入口点注册到[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数，则当 NDIS 调用*MiniportSetOptions*时，驱动程序可能以前从注册表获取了这些参数。

     

2.  如果启用了 SR-IOV，则 PF 微型端口驱动程序会将网络适配器配置为带有 NIC 交换机参数的注册表。 在配置网络适配器之前，驱动程序必须验证参数是否有效。 例如，微型端口驱动程序必须验证分配给 NIC 交换机的 PCIe 虚拟函数（VFs）的最大数量是否不超过网络适配器支持的 VFs 的数目。

3.  微型端口驱动程序调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)以启用 sr-iov，并在网络适配器上设置 VFs 的数目。 此函数配置适配器 PCI 配置空间中的 SR-IOV 扩展功能。 如果此函数返回 NDIS\_状态\_SUCCESS，则启用 SR-IOV，并通过 PCIe 接口公开 VFs。

**请注意**  如果 PF 微型端口驱动程序以静态方式创建 NIC 交换机，则在 NDIS\_\_NIC 的对象标识符（OID）方法请求发出 OID 时，不能使用该开关[\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)。 如果 PF 端口驱动程序静态创建了 NIC 交换机，则必须验证是否在 OID 请求中指定了开关参数。 这些参数（如[**NDIS\_NIC\_交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)与 OID 请求关联\_参数结构）必须与用于创建开关的驱动程序的参数相同。

 

有关如何处理[oid\_nic 的详细信息\_交换机\_创建\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)请求，请参阅[处理 oid\_NIC\_switch\_创建\_switch 请求](handling-the-oid-nic-switch-create-switch-request.md)。

若要详细了解 PF 微型端口驱动程序的初始化顺序和要求，请参阅[初始化 Pf 微型端口驱动程序](initializing-a-pf-miniport-driver.md)。

 

 






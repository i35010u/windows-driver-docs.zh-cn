---
title: NIC 交换机的静态创建
description: NIC 交换机的静态创建
ms.assetid: F325B1F8-7655-4044-AF04-32B434574082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 707521bf455cc965a666460a6925ef4219936991
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376761"
---
# <a name="static-creation-of-a-nic-switch"></a>NIC 交换机的静态创建


支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器必须能够创建 NIC 交换机。 对于某些适配器，NIC 开关可以创建以静态方式调用的上下文中[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)。

仅微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 的 SR-IOV 适配器可以在适配器上创建 NIC 开关。

**请注意**  从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。

 

通过在注册表中的标准化的关键字设置定义默认 NIC 开关参数。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

PF 微型端口驱动程序时 NDIS 调用驱动程序的静态创建的 NIC 交换机[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 通常情况下，驱动程序创建，并将 NIC 交换机配置为其初始化序列的一部分之前其网络适配器上启用 SR-IOV。

PF 微型端口驱动程序按照以下步骤时它会以静态方式创建 NIC 开关并为调用的上下文中的网络适配器上启用 SR-IOV [ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize):

1.  PF 微型端口驱动程序必须读取要确定是否启用了 SR-IOV，并获取配置参数的 NIC 交换机的 SR-IOV 标准化关键字。

    **请注意**  PF 微型端口驱动程序如果注册的入口点[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数，该驱动程序可能具有以前获取从这些参数注册表 NDIS 调用时*MiniportSetOptions*。

     

2.  如果启用了 SR-IOV，PF 微型端口驱动程序使用注册表中的 NIC 开关参数配置的网络适配器。 驱动程序必须验证其配置的网络适配器前参数有效。 例如，微型端口驱动程序必须验证分配给 NIC 交换机 PCIe 虚函数 (VFs) 的最大数目不会超过支持的网络适配器的 VFs 数。

3.  微型端口驱动程序调用[ **NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)启用 SR-IOV 和网络适配器上设置的 VFs 数。 此函数适配器的 PCI 配置空间中配置的 SR-IOV 扩展功能。 如果此函数返回 NDIS\_状态\_成功后，启用 SR-IOV 和 VFs 公开通过 PCIe 接口。

**请注意**  PF 微型端口驱动程序以静态方式创建 NIC 开关，如果不能使用开关，直到 NDIS 发出的一个对象标识符 (OID) 方法请求[OID\_NIC\_交换机\_创建\_交换机](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)。 如果 PF 微型端口驱动程序以静态方式创建 NIC 开关，它必须验证确保 OID 请求中指定开关参数。 这些参数，如包含在[ **NDIS\_NIC\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构与 OID 请求相关联，必须与相同该驱动程序使用来创建交换机的参数。

 

有关如何处理的详细信息[OID\_NIC\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)请求，请参阅[处理 OID\_NIC\_交换机\_创建\_切换请求](handling-the-oid-nic-switch-create-switch-request.md)。

初始化序列和 PF 微型端口驱动程序要求的详细信息，请参阅[初始化 PF 微型端口驱动程序](initializing-a-pf-miniport-driver.md)。

 

 






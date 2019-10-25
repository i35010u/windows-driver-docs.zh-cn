---
title: NIC 交换机的动态创建
description: NIC 交换机的动态创建
ms.assetid: 16B2D94A-AF30-434F-8F14-2F535501A52F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d0678d441e6e43670ebfcba70f1772cd9bc0f13
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834810"
---
# <a name="dynamic-creation-of-a-nic-switch"></a>NIC 交换机的动态创建


支持单根 i/o 虚拟化（SR-IOV）的网络适配器必须能够创建 NIC 交换机。 对于某些适配器，可以在微型端口驱动程序从对[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用返回后动态创建 NIC 交换机。

只有 SR-IOV 适配器的 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序可以在适配器上创建 NIC 交换机。

**注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为*默认 NIC 交换机*，由 NDIS\_默认\_交换机\_ID 标识符引用。

 

NDIS 发出 OID\_NIC 的对象标识符（OID）方法请求[\_交换机\_创建\_交换机](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)，以便在 sr-iov 网络适配器上创建 NIC 交换机。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)的指针，该指针包含用于开关的参数结构\_参数结构。

如果 PF 微型端口驱动程序支持动态 NIC 交换机创建，则它在处理此 OID 请求时必须遵循以下步骤：

1.  PF 小型端口驱动程序根据这些参数为 NIC 交换机分配必要的硬件和软件资源。 驱动程序还用这些参数配置网络适配器。

    **请注意**  PF 小型端口驱动程序支持动态 NIC 交换机创建，不必通过注册表中的标准化 sr-iov 关键字设置来读取开关参数。 NDIS 将读取这些关键字，以初始化[**NDIS\_nic\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构，然后将[OID 颁发\_nic\_switch\_创建\_switch](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)请求。 有关这些关键字的详细信息，请参阅[sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

     

2.  微型端口驱动程序调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)以启用 sr-iov，并在网络适配器上设置 VFs 的数目。 此函数配置适配器 PCI 配置空间中的 SR-IOV 扩展功能。 如果此函数返回 NDIS\_状态\_SUCCESS，则启用 SR-IOV，并通过 PCIe 接口公开 VFs。

有关如何处理[oid\_nic 的详细信息\_交换机\_创建\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)请求，请参阅[处理 oid\_NIC\_switch\_创建\_switch 请求](handling-the-oid-nic-switch-create-switch-request.md)。

 

 






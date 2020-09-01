---
title: NIC 交换机的动态创建
description: NIC 交换机的动态创建
ms.assetid: 16B2D94A-AF30-434F-8F14-2F535501A52F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72964ad3ea4823d303188ae2479358b14e1ffb62
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213971"
---
# <a name="dynamic-creation-of-a-nic-switch"></a>NIC 交换机的动态创建


支持单根 i/o 虚拟化 (SR-IOV) 的网络适配器必须能够创建 NIC 交换机。 对于某些适配器，可以在微型端口驱动程序从对 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用返回后动态创建 NIC 交换机。

只有 PCI Express (PCIe) 物理功能 (PF) 的微型端口驱动程序才能在适配器上创建 NIC 交换机。

**注意**   从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 *默认 NIC 交换机*，由 NDIS \_ 默认 \_ 交换机 \_ ID 标识符引用。

 

NDIS)  (OID 发出对象标识符，oid [ \_ NIC \_ 交换机 \_ CREATE \_ 开关](./oid-nic-switch-create-switch.md) 用于在 sr-iov 网络适配器上创建 NIC 交换机。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构的指针，该结构包含开关的参数。

如果 PF 微型端口驱动程序支持动态 NIC 交换机创建，则它在处理此 OID 请求时必须遵循以下步骤：

1.  PF 小型端口驱动程序根据这些参数为 NIC 交换机分配必要的硬件和软件资源。 驱动程序还用这些参数配置网络适配器。

    **注意**   支持动态 NIC 交换机创建的 PF 微型端口驱动程序不必通过注册表中的标准化 SR-IOV 关键字设置来读取开关参数。 NDIS 在颁发[OID \_ nic 交换机 \_ \_ CREATE \_ SWITCH](./oid-nic-switch-create-switch.md)请求之前，读取这些关键字以初始化[**NDIS \_ nic \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。 有关这些关键字的详细信息，请参阅 [sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

     

2.  微型端口驱动程序调用 [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) 以启用 sr-iov，并在网络适配器上设置 VFs 的数目。 此函数配置适配器 PCI 配置空间中的 SR-IOV 扩展功能。 如果此函数返回 NDIS \_ 状态 \_ 成功，则启用 sr-iov，并通过 PCIe 接口公开 VFs。

有关如何处理 [oid \_ nic \_ 交换机 \_ create \_ switch](./oid-nic-switch-create-switch.md) 请求的详细信息，请参阅 [处理 oid \_ nic \_ 交换机 \_ create \_ switch 请求](handling-the-oid-nic-switch-create-switch-request.md)。

 


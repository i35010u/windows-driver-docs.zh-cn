---
title: 创建 NIC 交换机
description: 创建 NIC 交换机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4413e4dc5cd6d1f56c4f7a76491e4d051c0da5e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821397"
---
# <a name="creating-a-nic-switch"></a>创建 NIC 交换机


本部分介绍了创建支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器的 NIC 交换机的要求和准则。 适用于 SR-IOV 网络适配器的 PCI Express (PCIe) 物理功能 (PF) 的微型端口驱动程序在适配器上创建和配置 NIC 交换机。

可以通过以下方法之一创建 NIC 交换机：

<a href="" id="static-creation"></a>静态创建  
通过使用注册表设置定义的一组交换机参数，在 SR-IOV 网络适配器上静态创建 NIC 交换机。 创建 NIC 交换机后，当驱动程序正在运行时，不能更改其参数。

PF 小型端口驱动程序在调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数的上下文中静态创建 NIC 交换机。 但是，在 NDIS 发出对象标识符 (OID) 方法请求 [oid \_ nic \_ 交换机 \_ CREATE \_ switch](./oid-nic-switch-create-switch.md)之前，不能使用 NIC 开关。 即使之前创建了 NIC 交换机，PF 微型端口驱动程序也启用了 NIC 交换机，以便在处理此 OID 请求时使用。

有关此方法的详细信息，请参阅 [静态创建 NIC 交换机](static-creation-of-a-nic-switch.md)。

<a href="" id="dynamic-creation"></a>动态创建  
NIC 交换机通过 oid [ \_ NIC \_ 交换机 \_ CREATE \_ switch](./oid-nic-switch-create-switch.md)的 oid 方法请求在 sr-iov 网络适配器上动态创建。 此 OID 请求通过 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构来定义 NIC 交换机参数。 这些参数也基于 staticallydefined 注册表设置，但在微型端口驱动程序运行时可能会动态变化。

有关此方法的详细信息，请参阅 [动态创建 NIC 交换机](dynamic-creation-of-a-nic-switch.md)。

有关如何处理 [oid \_ nic \_ 交换机 \_ create \_ switch](./oid-nic-switch-create-switch.md) 请求的详细信息，请参阅 [处理 oid \_ nic \_ 交换机 \_ create \_ switch 请求](handling-the-oid-nic-switch-create-switch-request.md)。

有关 SR-IOV 网络适配器的 NIC 交换机的详细信息，请参阅 [Nic 交换机](nic-switches.md)。

**注意**  在 SR-IOV 网络适配器上 (VF) 的 PCIe 虚拟功能的微型端口驱动程序不会创建或配置网络适配器的硬件资源，如 NIC 交换机。 有关详细信息，请参阅 [编写 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 


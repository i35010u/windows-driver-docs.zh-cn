---
title: 创建 NIC 交换机
description: 创建 NIC 交换机
ms.assetid: 5A184EBD-95F4-4C11-AACD-49DF04578CA0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f6e183eb75ffdf0fa90329a3cb4837f76b972a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835036"
---
# <a name="creating-a-nic-switch"></a>创建 NIC 交换机


本部分介绍创建支持单个根 i/o 虚拟化（SR-IOV）的网络适配器的 NIC 交换机的要求和准则。 SR-IOV 网络适配器的 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序会在适配器上创建和配置 NIC 交换机。

可以通过以下方法之一创建 NIC 交换机：

<a href="" id="static-creation"></a>静态创建  
通过使用注册表设置定义的一组交换机参数，在 SR-IOV 网络适配器上静态创建 NIC 交换机。 创建 NIC 交换机后，当驱动程序正在运行时，不能更改其参数。

PF 小型端口驱动程序在调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的上下文中静态创建 NIC 交换机。 但是，在 NDIS 发出 OID\_\_的对象标识符（OID）方法请求时，无法使用 NIC 交换机[\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)。 即使之前创建了 NIC 交换机，PF 微型端口驱动程序也启用了 NIC 交换机，以便在处理此 OID 请求时使用。

有关此方法的详细信息，请参阅[静态创建 NIC 交换机](static-creation-of-a-nic-switch.md)。

<a href="" id="dynamic-creation"></a>动态创建  
NIC 交换机通过 oid 的 oid 方法请求在 SR-IOV 网络适配器上动态创建， [\_NIC\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)。 此 OID 请求通过 NDIS\_NIC 定义 NIC 交换机参数[ **\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。 这些参数也基于 staticallydefined 注册表设置，但在微型端口驱动程序运行时可能会动态变化。

有关此方法的详细信息，请参阅[动态创建 NIC 交换机](dynamic-creation-of-a-nic-switch.md)。

有关如何处理[oid\_nic 的详细信息\_交换机\_创建\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)请求，请参阅[处理 oid\_NIC\_switch\_创建\_switch 请求](handling-the-oid-nic-switch-create-switch-request.md)。

有关 SR-IOV 网络适配器的 NIC 交换机的详细信息，请参阅[Nic 交换机](nic-switches.md)。

**请注意**  sr-iov 网络适配器上的 PCIe 虚拟功能（VF）的微型端口驱动程序不会创建或配置网络适配器的硬件资源（例如 NIC 交换机）。 有关详细信息，请参阅[编写 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 






---
title: 创建 NIC 交换机
description: 创建 NIC 交换机
ms.assetid: 5A184EBD-95F4-4C11-AACD-49DF04578CA0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ff47db9ba34ed09ae834397eae554c7aa63ebca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357371"
---
# <a name="creating-a-nic-switch"></a>创建 NIC 交换机


本部分介绍的要求和有关创建支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器上的 NIC 开关的指导。 微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 的 SR-IOV 网络适配器的创建，并在适配器上配置的 NIC 交换机。

可以通过以下方法之一创建 NIC 开关：

<a href="" id="static-creation"></a>静态创建  
NIC 是以静态方式创建交换机 SR-IOV 网络适配器上使用一组定义的注册表设置的开关参数。 创建 NIC 开关后，该驱动程序正在运行时，也不能更改其参数。

PF 微型端口驱动程序以静态方式创建的驱动程序的调用上下文中的 NIC 交换机[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 直到 NDIS 发出的一个对象标识符 (OID) 方法请求但不能使用 NIC 开关[OID\_NIC\_切换\_创建\_切换](https://msdn.microsoft.com/library/windows/hardware/hh451815)。 即使以前创建的 NIC 交换机，PF 微型端口驱动程序处理此 OID 请求时，启用使用 NIC 开关。

有关此方法的详细信息，请参阅[静态创建的 NIC 交换机](static-creation-of-a-nic-switch.md)。

<a href="" id="dynamic-creation"></a>动态创建  
通过 OID 方法请求的 SR-IOV 网络适配器上动态创建的 NIC 交换机[OID\_NIC\_切换\_创建\_切换](https://msdn.microsoft.com/library/windows/hardware/hh451815)。 此 OID 请求定义 NIC 开关参数通过[ **NDIS\_NIC\_切换\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)结构。 这些参数还基于 staticallydefined 注册表设置，但无法微型端口驱动程序运行时动态更改。

有关此方法的详细信息，请参阅[动态创建的 NIC 交换机](dynamic-creation-of-a-nic-switch.md)。

有关如何处理的详细信息[OID\_NIC\_交换机\_创建\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451815)请求，请参阅[处理 OID\_NIC\_交换机\_创建\_切换请求](handling-the-oid-nic-switch-create-switch-request.md)。

SR-IOV 网络适配器的 NIC 开关的详细信息，请参阅[NIC 开关](nic-switches.md)。

**请注意**  微型端口驱动程序为 PCIe 虚拟函数 (VF) 的 SR-IOV 网络适配器上不创建或配置网络适配器的硬件资源，例如 NIC 开关。 有关详细信息，请参阅[编写的 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 






---
title: NIC 交换机的动态创建
description: NIC 交换机的动态创建
ms.assetid: 16B2D94A-AF30-434F-8F14-2F535501A52F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeb05d7d6481c23cc43df34bb7f43645e66a8bf3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372641"
---
# <a name="dynamic-creation-of-a-nic-switch"></a>NIC 交换机的动态创建


支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器必须能够创建 NIC 交换机。 对于某些适配器，NIC 开关可动态创建微型端口驱动程序已从调用返回后[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)。

仅微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 的 SR-IOV 适配器可以在适配器上创建 NIC 开关。

**请注意**  从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。

 

NDIS 发出的一个对象标识符 (OID) 方法请求[OID\_NIC\_切换\_创建\_切换](https://msdn.microsoft.com/library/windows/hardware/hh451815)SR-IOV 网络适配器上创建一个 NIC 开关。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_切换\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)结构，其中包含为开关参数。

如果 PF 微型端口驱动程序支持动态 NIC 开关创建的当处理此 OID 请求时，它必须执行以下步骤：

1.  PF 微型端口驱动程序为基于这些参数的 NIC 交换机分配所需的硬件和软件资源。 该驱动程序还使用以下参数配置的网络适配器。

    **请注意**  PF 微型端口驱动程序支持动态 NIC 开关创建无需读取注册表中的标准化 SR-IOV 关键字设置通过在开关参数。 NDIS 读取这些关键字来初始化[ **NDIS\_NIC\_交换机\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451587)结构才能发出[OID\_NIC\_交换机\_创建\_交换机](https://msdn.microsoft.com/library/windows/hardware/hh451815)请求。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

     

2.  微型端口驱动程序调用[ **NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)启用 SR-IOV 和网络适配器上设置的 VFs 数。 此函数适配器的 PCI 配置空间中配置的 SR-IOV 扩展功能。 如果此函数返回 NDIS\_状态\_成功后，启用 SR-IOV 和 VFs 公开通过 PCIe 接口。

有关如何处理的详细信息[OID\_NIC\_交换机\_创建\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451815)请求，请参阅[处理 OID\_NIC\_交换机\_创建\_切换请求](handling-the-oid-nic-switch-create-switch-request.md)。

 

 






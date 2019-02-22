---
title: 删除 NIC 开关
description: 删除 NIC 开关
ms.assetid: BCC6A38B-F25B-483A-B9FF-D6FF73F9B2F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d35b1913ce7845cdf9d89aff75b55340721e2a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526143"
---
# <a name="deleting-a-nic-switch"></a>删除 NIC 开关


支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器必须能够删除 NIC 交换机。 仅微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 的 SR-IOV 适配器可以删除该适配器上的 NIC 交换机。

**请注意**  开头 NDIS 6.30 Windows Server 2012 中，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。

 

正在停止 PF 微型端口驱动程序之前, NDIS 删除 NIC 开关通过发出的对象标识符 (OID) 组请求[OID\_NIC\_切换\_删除\_切换](https://msdn.microsoft.com/library/windows/hardware/hh451817)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_切换\_删除\_切换\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451575)结构，它指定要删除的交换机的标识符。

NDIS 强制实施以下策略之前发出 OID 设置的请求[OID\_NIC\_交换机\_删除\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451817)到 PF 微型端口驱动程序：

-   NDIS 保证所有接收筛选器已被清除从默认和非默认 NIC 交换机上的虚拟端口 (VPorts)。 接收通过 OID 集请求的清除筛选器[OID\_接收\_筛选器\_清除\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569785)。

-   NDIS 保证，所有非默认虚拟端口 (VPorts) 交换机上创建之前已删除。 通过的 OID 集请求删除 VPorts [OID\_NIC\_交换机\_删除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)。

-   NDIS 保证已之前释放所有资源的 PCIe 虚拟函数 (VFs) 连接到该 NIC 交换机。 通过 OID 集请求的释放 VFs [OID\_NIC\_交换机\_免费\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)。

当它收到的 OID 方法请求[OID\_NIC\_交换机\_删除\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451817)，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态创建和配置的 NIC 开关，它必须释放与指定的 NIC 交换机相关联的软件资源。 但是，该驱动程序可以仅免费的硬件资源的 NIC 切换时[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)调用。

    有关静态 NIC 交换机创建的详细信息，请参阅[静态创建的 NIC 切换](static-creation-of-a-nic-switch.md)。

2.  如果 PF 微型端口驱动程序支持的动态创建和配置的 NIC 开关，它必须释放与指定的 NIC 交换机相关联的硬件和软件资源。

    有关动态 NIC 交换机创建的详细信息，请参阅[动态创建的 NIC 切换](dynamic-creation-of-a-nic-switch.md)。

3.  如果 PF 微型端口驱动程序上的网络适配器支持的动态创建 NIC 的开关和所有已删除的 NIC 开关，该驱动程序必须通过调用禁用适配器上的虚拟化[ **NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481). 若要禁用虚拟化，网络适配器必须设置*EnableVirtualization*为 FALSE 的参数和*NumVFs*参数为零。

    [**NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)清除**NumVFs**成员并**VF 启用**位的 SR-IOV 扩展功能结构中的 PCIe 配置空间网络适配器的 PF.

    **请注意**  PF 微型端口驱动程序支持静态创建和配置的 NIC 开关，如果它必须仅调用[ **NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)时[*MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)调用。

     

 

 






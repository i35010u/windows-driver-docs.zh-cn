---
title: 枚举网络适配器上的虚拟端口
description: 枚举网络适配器上的虚拟端口
ms.assetid: 437C3356-4CC7-4128-9E61-FD01157F4FD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8c088c83181f0372064df478fceac45f1f320aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352967"
---
# <a name="enumerating-virtual-ports-on-a-network-adapter"></a>枚举网络适配器上的虚拟端口


基础驱动程序或用户应用程序可以获取 NIC 支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器的交换机上的所有虚拟端口 (VPorts) 的列表。 驱动程序或应用程序发出的对象标识符 (OID) 方法请求[OID\_NIC\_交换机\_枚举\_VPORTS](https://msdn.microsoft.com/library/windows/hardware/hh451821)来获取此列表。

通过此 OID 查询请求的成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向包含以下各项的缓冲区的指针：

-   [ **NDIS\_NIC\_交换机\_VPORT\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451595)结构，用于定义数组中元素数。

-   一个数组[ **NDIS\_NIC\_交换机\_VPORT\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451594)结构。 每个这些结构包含有关 VPort 网络适配器的 NIC 交换机上的信息。

    **请注意**  如果在网络适配器上未不创建任何 VPorts，驱动程序设置**NumElements**的成员[ **NDIS\_NIC\_开关\_VPORT\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451595)为零，并无结构[ **NDIS\_NIC\_交换机\_VPORT\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/hh451594)返回结构。

     

过量的驱动程序或用户应用程序问题之前[OID\_NIC\_交换机\_枚举\_VPORTS](https://msdn.microsoft.com/library/windows/hardware/hh451821)请求，它必须初始化[ **NDIS\_NIC\_交换机\_VPORT\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh451595)随请求一起传递的结构。 驱动程序或应用程序初始化时，必须遵循这些准则**NDIS\_NIC\_交换机\_VPORT\_信息\_数组**结构：

-   如果 NDIS\_NIC\_交换机\_VPORT\_信息\_数组\_枚举\_ON\_特定\_中设置了开关标志**标志**成员，则返回的信息为所有 VPorts 都创建指定 NIC 交换机上。 通过指定 NIC 开关**SwitchId**该结构的成员。

    **请注意**  从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。 无论在中设置的标志**标志**成员**SwitchId**成员必须设置为 NDIS\_默认\_开关\_id。

     

-   如果 NDIS\_NIC\_交换机\_VPORT\_信息\_数组\_枚举\_ON\_特定\_中设置函数标志**标志**成员，则返回的信息为所有 VPorts 都附加到指定 PCI Express (PCIe) 物理函数 (PF) 或虚拟函数 (VF) 上的网络适配器。 通过指定 PF 或 VF **AttachedFunctionId**该结构的成员。

    如果**AttachedFunctionId**成员设置为 NDIS\_PF\_函数\_ID，对于所有 VPorts 返回信息。 这包括默认值附加到 PF.VPort 如果**AttachedFunctionId**成员设置为有效的 VF 标识符，信息为所有 VPorts 都附加到指定 VF 返回。

    **请注意**  从 Windows Server 2012，只有一个非默认 VPort 可以附加到 VF 开始。 但是，可以将多个 VPorts （包括默认 VPort） 附加到 PF.

     

-   如果**标志**成员设置为零，对于所有 VPorts 都附加到 PF 或 VF 上的网络适配器，将返回信息。 在本示例中的值**SwitchId**并**AttachedFunctionId**将被忽略。

NDIS 句柄[OID\_NIC\_交换机\_枚举\_VPORTS](https://msdn.microsoft.com/library/windows/hardware/hh451821)微型端口驱动程序的请求。 NDIS 从它所维护从检查以下源的数据的内部缓存中返回的信息：

-   OID 的方法请求[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。

-   设置的请求通过 OID [OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)。

 

 






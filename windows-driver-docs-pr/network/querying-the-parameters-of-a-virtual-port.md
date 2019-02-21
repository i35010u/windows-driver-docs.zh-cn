---
title: 查询的参数的虚拟端口
description: 查询的参数的虚拟端口
ms.assetid: 482DA041-2C70-438A-8D29-0F338CDCF935
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afb90e36f69cd108e752d3f30e2ff2a75dc0a54e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534629"
---
# <a name="querying-the-parameters-of-a-virtual-port"></a>查询的参数的虚拟端口


基础驱动程序可以获取支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器上的 NIC 交换机上的虚拟端口 (VPort) 的参数。 该驱动程序发出的一个对象标识符 (OID) 方法请求[OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)来获取这些参数。

基础驱动程序将发出此 OID 方法请求之前，必须将格式化[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构。 该驱动程序必须按以下方式设置此结构的成员：

-   **SwitchId**成员必须设置为 NIC 开关的参数为要返回的标识符。

    **请注意**  从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 交换机*。 **SwitchId**成员必须设置为 NDIS\_默认\_交换机\_id。

     

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 基础驱动程序将获取通过以下方式之一的 VPort 标识符：

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_枚举\_VPORTS](https://msdn.microsoft.com/library/windows/hardware/hh451821)。

通过此 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构。 此结构包含有关指定 VPort 的参数。

NDIS 句柄[OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)微型端口驱动程序的请求。 NDIS 从它所维护从检查以下源的数据的内部缓存中返回的信息：

-   OID 的方法请求[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。

-   设置的请求通过 OID [OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)。

 

 






---
title: 查询虚拟功能的参数
description: 查询虚拟功能的参数
ms.assetid: D834762D-9141-4F0F-B76D-5C8ABB016B64
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c2e2ca1b03bd73611583a102902e1455887a8ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339983"
---
# <a name="querying-the-parameters-of-a-virtual-function"></a>查询虚拟功能的参数


基础驱动程序或用户模式应用程序可以获取当前参数的 PCI Express (PCIe) 虚拟函数 (VF) 上支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器。 驱动程序或应用程序发出的对象标识符 (OID) 方法请求[OID\_NIC\_交换机\_VF\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451824)来获取这些参数。

基础驱动程序将发出此 OID 方法请求之前，必须将格式化[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。 驱动程序或应用程序必须设置**VFId**成员添加到为其参数是要返回的 VF 的标识符。 可以按以下方式获取 VF 标识符：

-   通过发出的 OID 方法请求[OID\_NIC\_交换机\_枚举\_VFS](https://msdn.microsoft.com/library/windows/hardware/hh451820)。

    如果已成功完成此 OID 请求，则基础驱动程序或用户模式应用程序接收所有 VFs 上的网络适配器分配的列表。 在列表中的每个元素均[ **NDIS\_NIC\_交换机\_VF\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451591)的结构，其中指定VF标识符**VFId**成员。

-   通过发出的 OID 方法请求[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)。

    如果已成功完成此 OID 请求，则基础驱动程序接收的标识符中新创建的 VF **VFId**所返回的成员[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。

    **请注意**  仅过量驱动程序可以获取这种方式中的取景器标识符。

     

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。 此结构包含有关指定 VF 配置参数。

NDIS 句柄[OID\_NIC\_交换机\_VF\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451824)微型端口驱动程序的请求。 NDIS 从它所维护从检查以下源的数据的内部缓存中返回的信息：

-   OID 的方法请求[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)。

-   设置的请求通过 OID [OID\_NIC\_交换机\_VF\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451824)。

 

 






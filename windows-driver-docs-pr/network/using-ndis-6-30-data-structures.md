---
title: 使用 NDIS 6.30 数据结构
description: 使用 NDIS 6.30 数据结构
ms.assetid: 0CAD1CCE-5AF6-4EBD-85C9-040FA0D1C141
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 466e7bf9dc2851e8f3aa9850cd004764f8865bf5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577451"
---
# <a name="using-ndis-630-data-structures"></a>使用 NDIS 6.30 数据结构


NDIS 可以支持多个版本的相同的数据结构。 对于 Windows 8 和 Windows Server 2012 操作系统，请使用 NDIS 6.30 版本的一种结构的微型端口驱动程序必须初始化**标头**具有正确的版本和大小的值结构的成员。 **标头**成员是[ **NDIS\_对象\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566588)结构和驱动程序必须初始化**修订**成员和**大小**的成员值**标头**成员添加到 NDIS 6.30 版本和大小的值。

**请注意**  来确定正确的版本和大小信息，请参阅每个结构，其中包含的参考页**标头**成员。 结构中包含的参考页**标头**成员并且已更新 NDIS 6.30 包括 NDIS 6.30 驱动程序的新信息。 如果不会更新到结构的 NDIS 6.30，早期 NDIS 版本提供的信息也适用于 NDIS 6.30 驱动程序。

 

有关 NDIS 6.30 更新了以下结构：

- [**NDIS\_BIND\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff564832)
- [**NDIS\_微型端口\_适配器\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565920)
- [**NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)
- [**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)
- [**NDIS\_微型端口\_适配器\_本机\_802\_11\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565926)
- [**NDIS\_NET\_BUFFER\_LIST\_FILTERING\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff566567)
- [**NDIS\_NIC\_交换机\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)
- [**NDIS\_OFFLOAD**](https://msdn.microsoft.com/library/windows/hardware/ff566705)
- [**NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706)
- [**NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)
- [**NDIS\_PM\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff566759)
- [**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff566864)
- [**NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)
- [**NDIS\_RECEIVE\_FILTER\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567181)
- [**NDIS\_接收\_队列\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567204)
- [**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567211)
- [**NDIS\_接收\_规模\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff567220)
- [**NDIS\_RSS\_处理器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567274)
- [**NDIS\_共享\_内存\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567303)
 

 






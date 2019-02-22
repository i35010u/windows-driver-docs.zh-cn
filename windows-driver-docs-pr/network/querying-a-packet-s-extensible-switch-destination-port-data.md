---
title: 查询数据包的可扩展交换机目标端口数据
description: 查询数据包的可扩展交换机目标端口数据
ms.assetid: 57D82C5E-3758-492C-A1DA-B7BC3DBE2E7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29801591a0c6991162e44a04c5e48d9c2d679196
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522041"
---
# <a name="querying-a-packets-extensible-switch-destination-port-data"></a>查询数据包的可扩展交换机目标端口数据


通过指定每个 HYPER-V 可扩展交换机目标端口[ **NDIS\_切换\_端口\_目标**](https://msdn.microsoft.com/library/windows/hardware/hh598224)中的元素[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)结构。 此数组包含在带外 (OOB) 转发的数据包的上下文[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 在此上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展交换机扩展调用[ *GetNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598157)函数来获取的指针[ **NDIS\_切换\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)中的数据包的结构[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 各个[ **NDIS\_交换机\_端口\_目标**](https://msdn.microsoft.com/library/windows/hardware/hh598224)可以通过访问此结构中的元素[ **NDIS\_交换机\_端口\_目标\_处\_数组\_索引**](https://msdn.microsoft.com/library/windows/hardware/hh598225)宏。

若要提高性能，转发扩展可以调用[ *GrowNetBufferListDestinations* ](https://msdn.microsoft.com/library/windows/hardware/hh598158)函数而不是[ *GetNetBufferListDestinations*](https://msdn.microsoft.com/library/windows/hardware/hh598157)若要获取的指针[ **NDIS\_交换机\_转发\_目标\_数组**](https://msdn.microsoft.com/library/windows/hardware/hh598210)结构. 扩展执行此操作如果确定它需要为目标端口的数据包的 OOB 数据中的其他数组元素。 有关详细信息，请参阅[添加可扩展交换机目标将数据转到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)。

**请注意**  只有数据包从此可扩展交换机出口数据路径将包含目标端口信息。 有关详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

 

 

 






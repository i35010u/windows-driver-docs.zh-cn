---
title: 枚举 VMQ 上的筛选器
description: 枚举 VMQ 上的筛选器
ms.assetid: 6d5d8cb6-7bdf-488b-8fcd-7c6e78c4fb24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d8224e35ab0430119228e0b90fa5c0fa27cc3ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372459"
---
# <a name="enumerating-filters-on-a-vmq"></a>枚举 VMQ 上的筛选器





若要获取在接收队列设置的所有筛选器的列表，请过量驱动程序和应用程序可以使用[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)方法对象标识符 (OID) 的请求。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构最初包含一个指向[**NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构。 当设置格式**NDIS\_接收\_筛选器\_信息\_数组**结构、 基础驱动程序或应用程序必须设置**QueueId**为接收队列的标识符 (ID) 的成员。 按以下方式获取接收队列 ID:

-   基础驱动程序的早期 OID 方法请求从获取接收队列 ID 值[OID\_接收\_筛选器\_分配\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569784)或[OID\_接收\_筛选器\_枚举\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569788)。 该驱动程序还可以指定**NDIS\_默认\_接收\_队列\_ID**默认接收队列。

-   应用程序从较早的 OID 方法请求获取接收队列 ID 值[OID\_接收\_筛选器\_枚举\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569788)。 此外可以指定应用程序**NDIS\_默认\_接收\_队列\_ID**默认接收队列。

从 OID 方法请求的成功返回后[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)，则**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含的指针的已更新[ **NDIS\_接收\_筛选器\_INFO\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)后跟一个或多个结构[ **NDIS\_接收\_筛选器\_信息** ](https://msdn.microsoft.com/library/windows/hardware/ff567176)结构。 每个**NDIS\_接收\_筛选器\_信息**结构指定的筛选器，指定的接收队列上设置的 ID。

过量驱动程序或应用程序可以使用[OID\_接收\_筛选器\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569792)OID 方法请求以获取接收队列在某个特定筛选器的参数。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构最初包含一个指向[**NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。 为基础的驱动程序或应用程序格式**NDIS\_接收\_筛选器\_参数**结构通过设置**FilterId**成员为非零 ID其参数位于要返回的筛选器值。

**请注意**  过量的驱动程序从较早的 OID 方法请求获取筛选器 ID [OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)或[OID\_接收\_筛选器\_ENUM\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)。 应用程序可以获取筛选器 ID 只能从较早 OID 方法请求的 OID\_接收\_筛选器\_枚举\_筛选器。

 

NDIS 句柄[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)并[OID\_接收\_筛选器\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569792)方法 OID 请求微型端口驱动程序。 NDIS 从它来自数据的内部缓存中获取信息[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)OID 请求。

 

 






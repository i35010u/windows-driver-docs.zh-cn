---
title: 获取和更新 VM 队列参数
description: 获取和更新 VM 队列参数
ms.assetid: 42beceec-95ae-48e3-985f-b6ee8a84d68b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd2785e9edb50c240fc0ee6f9a3a8b920eda919f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384255"
---
# <a name="obtaining-and-updating-vm-queue-parameters"></a>获取和更新 VM 队列参数





它分配后，基础驱动程序可以设置 VM 队列的配置参数。 此外，基础的驱动程序或应用程序可以获取队列的当前参数和参数在队列设置的筛选器可以。

若要更改队列的当前配置参数，过量驱动程序可以使用[OID\_接收\_筛选器\_队列\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569794)集 OID 请求。 基础驱动程序提供一个指针指向[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。

NDIS\_接收\_队列\_中使用参数结构[OID\_接收\_筛选器\_分配\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569784)OID 和[OID\_接收\_筛选器\_队列\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569794)OID。 有关分配队列的详细信息，请参阅[分配 VM 队列](allocating-a-vm-queue.md)。

若要获取当前配置的队列，过量驱动程序参数可以使用 OID\_接收\_筛选器\_队列\_参数方法 OID 请求。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构最初包含一个指向[**NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构类型 NDIS 队列标识符\_接收\_队列\_Id。 通过 OID 方法请求成功返回后**InformationBuffer**成员的 NDIS\_OID\_请求结构包含一个指向**NDIS\_接收\_队列\_参数**结构。

NDIS 处理微型端口驱动程序的方法请求。 因此，OID\_接收\_筛选器\_队列\_参数方法 OID 请求未请求的微型端口驱动程序。 NDIS 从 OID 从它收到的数据的内部缓存中获取信息\_接收\_筛选器\_分配\_队列和 OID\_接收\_筛选器\_队列\_参数 OID 请求。

若要获取当前的配置参数的过量驱动程序可以接收队列中的筛选器使用[OID\_接收\_筛选器\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569792)方法 OID 请求。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构最初包含一个指向[**NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。 使用 NDIS **FilterId**输入结构中的成员，若要标识筛选器。 从方法请求成功返回后**InformationBuffer**成员的 NDIS\_OID\_请求结构包含一个指向已更新的 NDIS\_接收\_筛选器\_参数结构。

NDIS 处理 OID\_接收\_筛选器\_参数方法 OID 请求微型端口驱动程序。 NDIS 从它来自数据的内部缓存中获取信息[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)OID 请求。

过量驱动程序可以使用 OID\_接收\_筛选器\_参数方法 OID 为接收队列中的筛选器获取配置参数的请求。

基础驱动程序从早期的 OID 获取筛选器标识符\_接收\_筛选器\_设置\_筛选器方法 OID 请求或从[OID\_接收\_筛选器\_ENUM\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)OID 请求。 只有驱动程序可以使用 OID\_接收\_筛选器\_设置\_筛选请求。

应用程序获取中的筛选器标识符[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)OID 请求。

 

 






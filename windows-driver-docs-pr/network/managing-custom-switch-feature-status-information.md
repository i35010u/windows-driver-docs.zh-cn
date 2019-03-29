---
title: 管理自定义交换机功能状态信息
description: 管理自定义交换机功能状态信息
ms.assetid: A1D561CC-22D8-47B6-9D95-6294B2998F3E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 228382aab92f39c7b72a618ec782ffc5bb9365c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562938"
---
# <a name="managing-custom-switch-feature-status-information"></a>管理自定义交换机功能状态信息


HYPER-V 可扩展交换机接口为可扩展交换机使用查询自定义状态信息的以下对象标识符 (OID)。 此状态信息被称为*切换功能状态*信息：

<a href="" id="oid-switch-feature-status-query"></a>[OID\_交换机\_功能\_状态\_查询](https://msdn.microsoft.com/library/windows/hardware/hh598260)  
获取指定的交换机属性的自定义功能状态信息的可扩展交换机的协议边缘颁发此 OID 方法请求。

通过此 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_交换机\_功能\_状态\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598208)结构，它指定要自定义功能状态信息返回。

    **请注意**  的自定义功能状态**FeatureStatusType**成员设置为**NdisSwitchPropertyTypeCustom**。

     

-   [ **NDIS\_交换机\_功能\_状态\_自定义**](https://msdn.microsoft.com/library/windows/hardware/hh598207)结构，其中包含有关分配给自定义属性的状态信息可扩展交换机端口。

    当发出可扩展交换机的协议边缘[OID\_切换\_功能\_状态\_查询](https://msdn.microsoft.com/library/windows/hardware/hh598260)请求，它会设置**FeatureStatusCustomBufferLength**并**FeatureStatusCustomBufferOffset**中的某个位置的成员**InformationBuffer**扩展插件可以使用到的成员返回功能的状态信息。

当它收到的 OID 方法请求时，可扩展交换机扩展必须遵循这些准则[OID\_切换\_功能\_状态\_查询](https://msdn.microsoft.com/library/windows/hardware/hh598260):

-   扩展必须处理 OID 请求，如果它管理匹配的自定义可扩展交换机功能状态**FeatureStatusId**的成员[ **NDIS\_切换\_功能\_状态\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598208)结构。

-   如果该扩展处理 OID 方法请求，它必须返回由指定的参数匹配的功能状态信息[ **NDIS\_交换机\_功能\_状态\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598208)结构。

    如果功能状态缓冲区太小，该扩展必须故障 OID 请求使用 NDIS\_状态\_无效\_长度。 扩展必须设置**数据。设置\_信息。BytesNeeded**中的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)是必需的最小缓冲区大小的结构。

    否则为该扩展必须返回功能的状态信息并完成 OID 请求使用 NDIS\_状态\_成功。

-   如果扩展不管理自定义可扩展交换机功能状态，它必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830)可扩展交换机在驱动程序堆栈的下层 OID 请求转发。

    有关如何将请求转发 OID 的详细信息，请参阅[NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

有关如何定义和注册交换机功能的状态信息的详细信息，请参阅[自定义切换功能状态](custom-switch-feature-status.md)。

 

 






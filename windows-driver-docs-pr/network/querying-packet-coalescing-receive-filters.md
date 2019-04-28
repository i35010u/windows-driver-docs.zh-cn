---
title: 查询数据包合并接收筛选器
description: 查询数据包合并接收筛选器
ms.assetid: D0B41718-37B9-4FB4-BA10-20765F836214
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a91050334c16928f908ed9b1139bf03c95e7af8a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339992"
---
# <a name="querying-packet-coalescing-receive-filters"></a>查询数据包合并接收筛选器





基础驱动程序和应用程序可以查询数据包合并接收通过执行以下操作下载到微型端口驱动程序的筛选器：

-   通过发出 OID 方法请求的请求的微型端口驱动程序上的接收筛选器的枚举的列表[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)。 有关详细信息，请参阅[枚举微型端口驱动程序上的接收筛选器](#enumerating)。

-   通过发出 OID 方法请求的请求微型端口驱动程序上的接收筛选器的测试条件参数[OID\_接收\_筛选器\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569792)。 有关详细信息，请参阅[查询微型端口驱动程序上的接收筛选器](#querying)

NDIS 句柄[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)并[OID\_接收\_筛选器\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569792)方法 OID 请求微型端口驱动程序。 NDIS 从它来自数据的内部缓存中获取信息[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)OID 请求。

## <a name="enumerating-the-receive-filters-on-a-miniport-driver"></a>枚举微型端口驱动程序上的接收筛选器


若要获取所有数据包合并接收的列表的已下载到微型端口驱动程序筛选器，基础驱动程序和应用程序发出的 OID 方法请求[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构。

**请注意**  过量的驱动程序或应用程序时初始化[ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构，它必须设置**QueueId**成员添加到 NDIS\_默认\_接收\_队列\_id。

 

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构，它指定当前配置的接收筛选器的列表微型端口驱动程序。

-   一个数组[ **NDIS\_接收\_筛选器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567176)微型端口驱动程序当前配置的接收筛选器有关的结构。

## <a name="querying-the-parameters-of-a-receive-filters-on-a-miniport-driver"></a>查询微型端口驱动程序接收的筛选器的参数


若要获取的参数的特定数据包合并接收已下载到微型端口驱动程序，过量驱动程序的筛选器或应用程序发出的 OID 方法请求[OID\_接收\_筛选器\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569792)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。 过量的驱动程序或应用程序初始化**NDIS\_接收\_筛选器\_参数**结构通过设置**FilterId**成员为非零 ID其参数位于要返回的筛选器值。

**请注意**  过量的驱动程序从较早的 OID 方法请求获取筛选器 ID [OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)或[OID\_接收\_筛选器\_ENUM\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)。 应用程序可以从较早的 OID OID 方法请求仅获取筛选器 ID\_接收\_筛选器\_枚举\_筛选器。

 

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181) ndis 指定的参数的结构接收筛选器。

-   一个数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构指定的筛选器测试条件中的一个字段网络数据包标头。

 

 






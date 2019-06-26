---
title: 查询数据包合并接收筛选器
description: 查询数据包合并接收筛选器
ms.assetid: D0B41718-37B9-4FB4-BA10-20765F836214
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c1250e4b0dce86c68d4a8a90eb5c74bb8e9583f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379197"
---
# <a name="querying-packet-coalescing-receive-filters"></a>查询数据包合并接收筛选器





基础驱动程序和应用程序可以查询数据包合并接收通过执行以下操作下载到微型端口驱动程序的筛选器：

-   通过发出 OID 方法请求的请求的微型端口驱动程序上的接收筛选器的枚举的列表[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。 有关详细信息，请参阅[枚举微型端口驱动程序上的接收筛选器](#enumerating-the-receive-filters-on-a-miniport-driver)。

-   通过发出 OID 方法请求的请求微型端口驱动程序上的接收筛选器的测试条件参数[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)。 有关详细信息，请参阅[查询微型端口驱动程序上的接收筛选器](#querying-the-parameters-of-a-receive-filters-on-a-miniport-driver)

NDIS 句柄[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)并[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)方法 OID 请求微型端口驱动程序。 NDIS 从它来自数据的内部缓存中获取信息[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID 请求。

## <a name="enumerating-the-receive-filters-on-a-miniport-driver"></a>枚举微型端口驱动程序上的接收筛选器


若要获取所有数据包合并接收的列表的已下载到微型端口驱动程序筛选器，基础驱动程序和应用程序发出的 OID 方法请求[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构。

**请注意**  过量的驱动程序或应用程序时初始化[ **NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，它必须设置**QueueId**成员添加到 NDIS\_默认\_接收\_队列\_id。

 

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指向缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，它指定当前配置的接收筛选器的列表微型端口驱动程序。

-   一个数组[ **NDIS\_接收\_筛选器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info)微型端口驱动程序当前配置的接收筛选器有关的结构。

## <a name="querying-the-parameters-of-a-receive-filters-on-a-miniport-driver"></a>查询微型端口驱动程序接收的筛选器的参数


若要获取的参数的特定数据包合并接收已下载到微型端口驱动程序，过量驱动程序的筛选器或应用程序发出的 OID 方法请求[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。 过量的驱动程序或应用程序初始化**NDIS\_接收\_筛选器\_参数**结构通过设置**FilterId**成员为非零 ID其参数位于要返回的筛选器值。

**请注意**  过量的驱动程序从较早的 OID 方法请求获取筛选器 ID [OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)或[OID\_接收\_筛选器\_ENUM\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。 应用程序可以从较早的 OID OID 方法请求仅获取筛选器 ID\_接收\_筛选器\_枚举\_筛选器。

 

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指向缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) ndis 指定的参数的结构接收筛选器。

-   一个数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构指定的筛选器测试条件中的一个字段网络数据包标头。

 

 






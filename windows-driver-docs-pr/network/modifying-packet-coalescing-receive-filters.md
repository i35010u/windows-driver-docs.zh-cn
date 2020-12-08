---
title: 修改数据包合并接收筛选器
description: 修改数据包合并接收筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f210aa9f334782750ce20df2db453ee11ba3a56d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837675"
---
# <a name="modifying-packet-coalescing-receive-filters"></a>修改数据包合并接收筛选器


若要修改支持数据包合并的微型端口驱动程序上的接收筛选器，请执行以下步骤：

1.  为了获取已下载到微型端口驱动程序的所有数据包合并接收筛选器的列表，过量驱动程序会发出 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)的 oid 方法请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的指针。

    **注意**  当过量驱动程序或应用程序初始化 [**ndis \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array) 结构时，它必须将 **QueueId** 成员设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

    成功从 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)的 Oid 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向已更新的 [**ndis \_ 接收 \_ 筛选 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的指针，该结构后跟一个或多个 [**NDIS \_ 接收 \_ 筛选器 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)结构。 每个 **NDIS \_ 接收 \_ 筛选 \_ 信息** 结构为网络适配器上设置的筛选器指定标识符 (ID) 。

2.  为了获取已下载到微型端口驱动程序的特定包合并接收筛选器的参数，过量驱动程序发出 oid [ \_ 接收 \_ 筛选器 \_ 参数](./oid-receive-filter-parameters.md)的 oid 方法请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 过量驱动程序或应用程序通过将 **FilterId** 成员设置为要返回其参数的筛选器的非零 ID 值来初始化 **NDIS \_ 接收 \_ 筛选器 \_ 参数** 结构。

    成功从 OID 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

    -   用于指定 NDIS 接收筛选器参数的 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构。

    -   用于为网络数据包标头中的一个字段指定筛选器测试条件的 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构的数组。

3.  过量驱动程序会修改接收筛选器，以添加、删除或更改筛选器的测试条件集。 驱动程序通过从 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构指定的字段参数数组添加、删除或修改单个 [**ndis \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构来实现此功能。

    当过量驱动程序已经完成对测试条件的修改时，它必须更新 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构的成员，以反映对接收筛选器所做的更改。 例如，过量驱动程序必须更新 **FieldParametersArrayNumElements** 成员，使其包含数组中新数量的元素。

    有关详细信息，请参阅 [指定数据包合并接收筛选器](specifying-a-packet-coalescing-receive-filter.md)。

4.  过量驱动程序发出 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md) 的 oid 方法请求，以将修改后的接收筛选器下载到微型端口驱动程序。

    有关详细信息，请参阅 [设置数据包合并接收筛选器](setting-a-packet-coalescing-receive-filter.md)。

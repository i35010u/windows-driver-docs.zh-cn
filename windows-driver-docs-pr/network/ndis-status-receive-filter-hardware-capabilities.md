---
title: NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES
description: 微型端口驱动程序在其硬件收到筛选功能更改时发出 NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES 状态指示。
ms.assetid: 12F7A736-D85A-4BB6-89E6-55195B76C29F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 73b659541b99df92f3a7b309a1af068be0d9480f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214662"
---
# <a name="ndis_status_receive_filter_hardware_capabilities"></a>NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能


微型端口驱动程序在其硬件收到筛选功能更改时发出 **NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能** 状态指示。 这些功能包括 INF 文件设置当前禁用的硬件功能，或通过 " **高级** 属性" 页禁用的硬件功能。

**注意**   此状态指示只应由支持 NDIS 接收筛选器的微型端口驱动程序来完成。

 

当微型端口驱动程序发出此状态指示时，它会将[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员设置为指向[**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的指针。 驱动程序将此结构初始化为其当前启用的接收筛选器功能。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](./ndis-packet-coalescing.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [管理包合并接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)。

-   [单个根 I/o 虚拟化 (sr-iov) ](./single-root-i-o-virtualization--sr-iov-.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置虚拟端口上的接收筛选器](./setting-a-receive-filter-on-a-virtual-port.md)。

-   [虚拟机队列 (VMQ)](./virtual-machine-queue--vmq--in-ndis-6-20.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](./setting-and-clearing-vmq-filters.md)。

如果满足以下条件之一，微型端口驱动程序会发出 **NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能** 状态指示：

-   硬件接收筛选器功能在单个网络适配器上发生更改。 例如，可以通过独立硬件供应商 (IHV) 开发的管理应用程序启用或禁用接收筛选器。

-   硬件接收筛选器功能更改了负载平衡故障转移 (LBFO) 由 MUX 中间驱动程序管理的网络适配器组。 例如，在组中添加或删除适配器时，硬件接收筛选器功能可能会更改。

    有关详细信息，请参阅 [NDIS MUX 中间驱动程序](./ndis-mux-intermediate-drivers.md)。

当微型端口驱动程序发出 **NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能** 状态指示时，请遵循以下步骤：

1.  小型端口将 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 的结构初始化为网络适配器上当前启用的接收筛选器功能。

    当微型端口驱动程序初始化**标题**成员时，它会将**标头**的**类型**成员设置为 NDIS \_ 对象 \_ 类型 \_ 默认值。 微型端口驱动程序将**标头**的**修订**成员设置为 ndis \_ 接收 \_ 筛选器 \_ 功能 \_ 修订版 \_ 2，并将**Size**成员设置为 ndis \_ SIZEOF \_ 接收 \_ 筛选器 \_ 功能 \_ 修订版本 \_ 2。

2.  微型端口驱动程序通过以下方式初始化状态指示的 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构：

    -   **StatusCode**成员必须设置为[**NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 当前 \_ 功能**](ndis-status-receive-filter-current-capabilities.md)。

    -   **StatusBuffer**成员必须设置为[**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的地址。

    -   **StatusBufferSize**成员必须设置为 `sizeof(NDIS_RECEIVE_FILTER_CAPABILITIES)` 。

3.  微型端口驱动程序通过调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)发出状态指示。 驱动程序必须将指向 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构的指针传递到 *StatusIndication* 参数。

**注意**   过量驱动程序可以使用**NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能**状态指示来确定当前启用的网络适配器接收筛选器功能。 此外，这些驱动程序还可以发出 oid 查询请求（ [oid \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能](./oid-receive-filter-hardware-capabilities.md) ），以便随时获取硬件接收筛选器功能。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)

[OID \_ 接收 \_ 筛选器 \_ 当前 \_ 功能](./oid-receive-filter-current-capabilities.md)

 


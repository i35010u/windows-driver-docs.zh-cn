---
title: NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES
description: 微型端口驱动程序发出 NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES 状态指示当其硬件收到筛选功能更改。
ms.assetid: 12F7A736-D85A-4BB6-89E6-55195B76C29F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RECEIVE_FILTER_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 44a3d2077a50a314800e1f0b69c492c828de6525
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385247"
---
# <a name="ndisstatusreceivefilterhardwarecapabilities"></a>NDIS\_状态\_接收\_筛选器\_硬件\_功能


微型端口驱动程序问题**NDIS\_状态\_接收\_筛选器\_硬件\_功能**状态指示当其硬件收到筛选功能更改。 这些功能包括由 INF 文件设置或通过当前已禁用的硬件功能**高级**属性页。

**请注意**  微型端口驱动程序支持 NDIS 接收筛选器应仅将此状态指示。

 

当微型端口驱动程序将此状态指示时，它会设置**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)为指向的结构[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。 此结构与当前已启用接收驱动程序初始化筛选功能。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下的 NDIS 接口中使用：

-   [NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 详细了解如何使用此接口中接收的筛选器，请参阅[管理数据包合并接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)。

-   [单根 I/O 虚拟化 (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 详细了解如何使用此接口中接收的筛选器，请参阅[上虚拟端口设置接收的筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)。

-   [虚拟机队列 (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 详细了解如何使用此接口中接收的筛选器，请参阅[设置和清除 VMQ 筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)。

微型端口驱动程序问题**NDIS\_状态\_接收\_筛选器\_硬件\_功能**状态指示以下条件之一时true:

-   硬件接收单一网络适配器上的筛选器功能更改。 例如，接收筛选器可以启用或禁用通过管理应用程序开发的独立硬件供应商 (IHV)。

-   硬件接收负载均衡由 MUX 中间驱动程序管理的网络适配器的故障转移 (LBFO) 团队的筛选器功能更改。 例如，硬件接收功能可能会更改时适配器添加到或从团队中删除的筛选器。

    有关详细信息，请参阅[NDIS MUX 中间驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)。

微型端口驱动程序按照以下步骤时它会发出**NDIS\_状态\_接收\_筛选器\_硬件\_功能**状态指示：

1.  微型端口初始化[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)上当前启用的接收筛选器功能的结构中的网络适配器。

    当微型端口驱动程序初始化**标头**成员，它会设置**类型**的成员**标头**到 NDIS\_对象\_类型\_默认值。 微型端口驱动程序集**修订**的成员**标头**到 NDIS\_接收\_筛选器\_功能\_修订\_2并**大小**成员添加到 NDIS\_SIZEOF\_接收\_筛选器\_功能\_修订\_2。

2.  微型端口驱动程序初始化[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构如下所示的状态指示：

    -   **StatusCode**成员必须设置为[ **NDIS\_状态\_接收\_筛选器\_当前\_功能**](ndis-status-receive-filter-current-capabilities.md).

    -   **StatusBuffer**成员必须设置为的地址[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

    -   **StatusBufferSize**成员必须设置为`sizeof(NDIS_RECEIVE_FILTER_CAPABILITIES)`。

3.  微型端口驱动程序问题的状态指示通过调用[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)。 该驱动程序必须传递一个指向[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构*StatusIndication*参数。

**请注意**  过量驱动程序可以使用**NDIS\_状态\_接收\_筛选器\_硬件\_功能**状态若要确定当前已启用的接收筛选器功能的网络适配器的指示。 或者，这些驱动程序还可以颁发的 OID 查询请求[OID\_接收\_筛选器\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)获取硬件接收筛选器功能任何时间。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)

[OID\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

 

 





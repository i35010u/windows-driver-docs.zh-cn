---
title: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS
description: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS 状态向 NDIS 和过量驱动程序表明，当前虚拟机 (VM) 队列参数在网络适配器上已更改。
ms.assetid: 30782C77-578F-4533-8B6B-9D2F64EE6189
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f83b7bc6ceb0481578109586777345ce0c3d4871
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212869"
---
# <a name="ndis_status_receive_filter_queue_parameters"></a>NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 队列 \_ 参数


**Ndis \_ 状态 \_ 接收 \_ 筛选器 \_ 队列 \_ 参数**状态向 ndis 和过量驱动程序表明，当前虚拟机 (VM) 队列参数在网络适配器上已更改。

<a name="remarks"></a>备注
-------

当当前 VM 队列参数在网络适配器上发生更改时，微型端口驱动程序必须发出 **NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 队列 \_ 参数** 状态指示。 如果满足以下条件之一，则 VM 队列参数可能会更改：

-   VM 队列参数通过独立硬件供应商 (IHV) 开发的管理应用程序进行更改。

-   VM 队列参数对于属于负载平衡故障转移的一个或多个网络适配器（ (LBFO) 由 MUX 中间驱动程序管理的团队）进行了更改。 有关详细信息，请参阅 [NDIS MUX 中间驱动程序](./ndis-mux-intermediate-drivers.md)。

当微型端口驱动程序发出 **NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 队列 \_ 参数** 状态指示时，必须执行以下步骤：

1.  微型端口驱动程序使用网络适配器上的当前 VM 队列参数初始化 [**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters) 结构。 驱动程序还必须使用相应**Flags**的 ndis \_ 接收 \_ 队列参数 Xxx 更改标志来设置此结构的标志成员 \_ \_ *Xxx* \_ ，以报告已更改的**ndis \_ 接收 \_ 队列 \_ 参数**成员值。

    **注意**  从 NDIS 6.30 开始，微型端口驱动程序只能发出 **ndis \_ 状态 \_ 接收 \_ 筛选器 \_ 队列 \_ 参数** 状态指示报告对 **InterruptCoalescingDomainId** 成员所做的更改。




当微型端口驱动程序初始化此结构的**标头**成员时，它会将**标头**的**类型**成员设置为 NDIS \_ 对象 \_ 类型 \_ 默认值。 微型端口驱动程序将**标头**的**修订**成员设置为 ndis \_ 接收 \_ 队列 \_ 参数 \_ 修订版本 \_ 2，并将**Size**成员设置为 ndis \_ SIZEOF \_ 接收 \_ 队列 \_ 参数 \_ 修订版本 \_ 2。


2.  微型端口驱动程序通过以下方式初始化 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构：

    -   **StatusCode**成员必须设置为**NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 队列 \_ 参数**。

    -   **StatusBuffer**成员必须设置为指向[**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的指针。 此结构包含 NIC 交换机当前启用的硬件功能。

    -   **StatusBufferSize**成员必须设置为 Sizeof ([**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)) 。

3.  微型端口驱动程序通过调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)发出状态通知。 驱动程序必须将指向 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构的指针传递到 *StatusIndication* 参数。

过量驱动程序可以使用 **NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 队列 \_ 参数** 状态指示来确定网络适配器上的当前 VM 队列参数。 此外，这些驱动程序还可以 (OID 发出对象标识符) 执行 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](oid-receive-filter-queue-parameters.md) 的查询请求，以随时获取这些参数。

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
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](oid-receive-filter-queue-parameters.md)
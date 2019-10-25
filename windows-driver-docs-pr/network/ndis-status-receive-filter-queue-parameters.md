---
title: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS
description: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS 状态向 NDIS 和过量驱动程序表明，当前虚拟机（VM）队列参数在网络适配器上已更改。
ms.assetid: 30782C77-578F-4533-8B6B-9D2F64EE6189
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d8fda407edcca4ff5814de5cabc0891694784505
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843521"
---
# <a name="ndis_status_receive_filter_queue_parameters"></a>\_接收\_筛选器\_队列\_参数的 NDIS\_状态


**\_接收\_筛选器\_\_队列的 ndis\_状态**向 ndis 和过量驱动程序指示当前的虚拟机（VM）队列参数在网络适配器上已更改。

<a name="remarks"></a>备注
-------

当当前 VM 队列参数在网络适配器上发生更改时，微型端口驱动程序必须发出**NDIS\_状态\_接收\_筛选器\_队列\_参数**状态指示。 如果满足以下条件之一，则 VM 队列参数可能会更改：

-   VM 队列参数通过独立硬件供应商（IHV）开发的管理应用程序进行更改。

-   对于属于 MUX 中间驱动程序管理的负载平衡故障转移（LBFO）团队的一个或多个网络适配器，VM 队列参数会发生变化。 有关详细信息，请参阅[NDIS MUX 中间驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)。

如果微型端口驱动程序发出**NDIS\_状态\_接收\_筛选器\_队列\_参数**状态指示，则必须执行以下步骤：

1.  微型端口驱动程序使用网络适配器上的当前 VM 队列参数初始化[**NDIS\_接收\_QUEUE\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构。 驱动程序还必须将此结构的**Flags**成员设置为相应的 NDIS\_接收\_队列\_参数\_*XXX*\_已更改的标志发送到**NDIS\_接收\_队列 @no__t**已更改的 _10_ 参数成员值。

    **注意** 从 NDIS 6.30 开始，微型端口驱动程序只能发出**ndis\_状态\_接收\_筛选器\_队列\_参数**状态指示报告对**InterruptCoalescingDomainId**成员所做的更改。




当微型端口驱动程序初始化此结构的**标头**成员时，它会将**标头**的**类型**成员设置为 NDIS\_对象\_类型\_默认值。 微型端口驱动程序将**标头**的**修订**成员设置为 NDIS\_接收\_队列\_参数\_修订版本\_2，并将**Size**成员设置为 NDIS\_SIZEOF\_RECEIVE\_QUEUE\_\_版本\_2 的参数。


2.  微型端口驱动程序通过以下方式初始化[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构：

    -   必须将**StatusCode**成员设置为**NDIS\_状态\_接收\_筛选器\_QUEUE\_参数**。

    -   必须将**StatusBuffer**成员设置为指向[**NDIS\_接收\_QUEUE\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的指针。 此结构包含 NIC 交换机当前启用的硬件功能。

    -   **StatusBufferSize**成员必须设置为 Sizeof （[**NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)）。

3.  微型端口驱动程序通过调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)发出状态通知。 驱动程序必须向*StatusIndication*参数传递指向[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。

过量驱动程序可以使用**NDIS\_状态\_接收\_筛选器\_队列\_参数**状态指示来确定网络适配器上的当前 VM 队列参数。 此外，这些驱动程序还可以发出[OID\_接收\_筛选器](oid-receive-filter-queue-parameters.md)的对象标识符（OID）查询请求，\_队列\_参数随时获取这些参数。

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
[**NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_接收\_筛选器\_队列\_参数](oid-receive-filter-queue-parameters.md)









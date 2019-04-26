---
title: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS
description: NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS 状态指示到 NDIS 和当前的虚拟机 (VM) 队列参数已更改的网络适配器的基础驱动程序。
ms.assetid: 30782C77-578F-4533-8B6B-9D2F64EE6189
ms.date: 08/08/2017
keywords: -NDIS_STATUS_RECEIVE_FILTER_QUEUE_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 463316f09dba21515a00594a7d256cfb8de65bd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330201"
---
# <a name="ndisstatusreceivefilterqueueparameters"></a>NDIS\_状态\_接收\_筛选器\_队列\_参数


**NDIS\_状态\_接收\_筛选器\_队列\_参数**状态指示到 NDIS 和基础驱动程序的当前虚拟机 (VM) 队列参数已更改的网络适配器上。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须发出**NDIS\_状态\_接收\_筛选器\_队列\_参数**状态指示当前的虚拟机队列参数具有时网络适配器上的更改。 当以下条件之一为 true 时，无法更改 VM 队列参数：

-   通过管理应用程序开发的独立硬件供应商 (IHV) 情况下，VM 队列参数已发生更改。

-   虚拟机队列参数更改为属于负载均衡由 MUX 中间驱动程序管理的故障转移 (LBFO) 团队的一个或多个网络适配器。 有关详细信息，请参阅[NDIS MUX 中间驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566498)。

当微型端口驱动程序发出**NDIS\_状态\_接收\_筛选器\_队列\_参数**状态指示，它必须执行以下步骤：

1.  微型端口驱动程序初始化[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)与网络适配器上的当前虚拟机队列参数的结构。 该驱动程序还必须设置**标志**成员的此结构与相应的 NDIS\_接收\_队列\_参数\_*Xxx* \_要报告的已更改的标志**NDIS\_接收\_队列\_参数**已更改的成员值。

    **请注意**NDIS 6.30 从开始，只能颁发微型端口驱动程序**NDIS\_状态\_接收\_筛选器\_队列\_参数**状态表示要报告将变为**InterruptCoalescingDomainId**成员。




当微型端口驱动程序初始化**标头**此结构的成员，它会设置**类型**的成员**标头**到 NDIS\_对象\_类型\_默认值。 微型端口驱动程序集**修订**的成员**标头**到 NDIS\_接收\_队列\_参数\_修订\_2 和**大小**成员添加到 NDIS\_SIZEOF\_接收\_队列\_参数\_修订\_2。


2.  微型端口驱动程序初始化[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构如下所示：

    -   **StatusCode**成员必须设置为**NDIS\_状态\_接收\_筛选器\_队列\_参数**。

    -   **StatusBuffer**成员必须设置为指向指针[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构。 此结构包含 NIC 开关的当前已启用的硬件功能。

    -   **StatusBufferSize**成员必须设置为 sizeof ([**NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211))。

3.  微型端口驱动程序通过调用发出状态通知[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)。 该驱动程序必须传递一个指向[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构*StatusIndication*参数。

过量驱动程序可以使用**NDIS\_状态\_接收\_筛选器\_队列\_参数**状态指示，以确定当前的 VM 上队列参数中的网络适配器。 或者，这些驱动程序还可以颁发对象标识符 (OID) 的查询请求[OID\_接收\_筛选器\_队列\_参数](oid-receive-filter-queue-parameters.md)以在任何时候获取这些参数。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567211)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_RECEIVE\_FILTER\_QUEUE\_PARAMETERS](oid-receive-filter-queue-parameters.md)









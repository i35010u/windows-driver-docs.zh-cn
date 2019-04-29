---
title: NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES
description: 微型端口驱动程序发出 NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES 状态指示其当前已启用的接收筛选功能更改时。
ms.assetid: 6A1141A3-6E46-4A97-B482-CBE69E3D5075
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 600f330141fdec96ac179db42aed178967535aaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362859"
---
# <a name="ndisstatusreceivefiltercurrentcapabilities"></a>NDIS\_状态\_接收\_筛选器\_当前\_功能


微型端口驱动程序问题**NDIS\_状态\_接收\_筛选器\_当前\_功能**状态指示其当前已启用接收时筛选功能更改。

**请注意**  微型端口驱动程序支持 NDIS 接收筛选器应仅将此状态指示。

 

当微型端口驱动程序将此状态指示时，它会设置**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)为指向的结构[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。 此结构与当前已启用接收驱动程序初始化筛选功能。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下的 NDIS 接口中使用：

-   [NDIS 数据包合并](https://msdn.microsoft.com/library/windows/hardware/hh451601)。 详细了解如何使用此接口中接收的筛选器，请参阅[管理数据包合并接收筛选器](https://msdn.microsoft.com/library/windows/hardware/hh464026)。

-   [单根 I/O 虚拟化 (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235)。 详细了解如何使用此接口中接收的筛选器，请参阅[上虚拟端口设置接收的筛选器](https://msdn.microsoft.com/library/windows/hardware/hh440224)。

-   [虚拟机队列 (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035)。 详细了解如何使用此接口中接收的筛选器，请参阅[设置和清除 VMQ 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff570780)。

微型端口驱动程序问题**NDIS\_状态\_接收\_筛选器\_当前\_功能**状态指示当以下条件之一为 true 时:

-   当前已启用接收单个网络适配器上的筛选器功能更改。 例如，接收筛选器可以启用或禁用通过管理应用程序开发的独立硬件供应商 (IHV)。

-   当前已启用接收功能更改筛选器适用于属于负载均衡由 MUX 中间驱动程序管理的故障转移 (LBFO) 团队的一个或多个网络适配器。 有关详细信息，请参阅[NDIS MUX 中间驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566498)。

微型端口驱动程序按照以下步骤时它会发出**NDIS\_状态\_接收\_筛选器\_当前\_功能**状态指示：

1.  微型端口初始化[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)上当前启用的接收筛选器功能的结构中的网络适配器。

    当微型端口驱动程序初始化**标头**成员，它会设置**类型**的成员**标头**到 NDIS\_对象\_类型\_默认值。 微型端口驱动程序集**修订**的成员**标头**到 NDIS\_接收\_筛选器\_功能\_修订\_2并**大小**成员添加到 NDIS\_SIZEOF\_接收\_筛选器\_功能\_修订\_2。

2.  微型端口驱动程序初始化[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构如下所示的状态指示：

    -   **StatusCode**成员必须设置为**NDIS\_状态\_接收\_筛选器\_当前\_功能**。

    -   **StatusBuffer**成员必须设置为的地址[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。

    -   **StatusBufferSize**成员必须设置为`sizeof(NDIS_RECEIVE_FILTER_CAPABILITIES)`。

3.  微型端口驱动程序问题的状态指示通过调用[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)。 该驱动程序必须传递一个指向[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构*StatusIndication*参数。

**请注意**  过量驱动程序可以使用**NDIS\_状态\_接收\_筛选器\_当前\_功能**状态指示若要确定当前已启用的接收筛选器功能的网络适配器。 或者，这些驱动程序还可以颁发的 OID 查询请求[OID\_接收\_筛选器\_当前\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569786)以获取当前已启用接收筛选器在任何时间的功能。

 

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
[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff566864)

[OID\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569786)

 

 





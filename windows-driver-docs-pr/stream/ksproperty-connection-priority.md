---
title: KSPROPERTY\_连接\_优先级
description: 客户端使用 KSPROPERTY\_连接\_优先级属性来获取或设置连接的优先级。
ms.assetid: 2037fe95-e176-4714-ad36-65a0e25b29e0
keywords:
- KSPROPERTY_CONNECTION_PRIORITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_PRIORITY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53ef527df994157b0da2f6775e7dd225589789ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826783"
---
# <a name="ksproperty_connection_priority"></a>KSPROPERTY\_连接\_优先级


客户端使用 KSPROPERTY\_连接\_优先级属性来获取或设置连接的优先级。

## <span id="ddk_ksproperty_connection_priority_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_PRIORITY_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspriority" data-raw-source="[&lt;strong&gt;KSPRIORITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspriority)"><strong>KSPRIORITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回包含优先级类和子类的[**KSPRIORITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspriority)类型的结构。

如果**PriorityClass**成员较大，或**PriorityClass**成员完全相同且**PrioritySubClass**成员较大，则优先级比另一个优先级大。

以下预定义的**PriorityClass**值可用： KSPRIORITY\_LOW、KSPRIORITY\_NORMAL、KSPRIORITY\_HIGH 和 KSPRIORITY\_EXCLUSIVE。 优先级默认为 KSPRIORITY\_NORMAL。 KSPRIORITY\_EXCLUSIVE 指示连接对 pin 使用的资源具有独占访问权限。

优先级值具有全局重要性：客户端可以使用报告的值在两个不相关的内核流式处理过滤器上设置两个不同的 pin 之间的优先级。

KSPROPERTY\_连接\_优先级是可选的。 客户端将不支持该端口的 pin 视为具有优先级 KSPRIORITY\_NORMAL。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPRIORITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspriority)

[**KSPIN\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)

 

 







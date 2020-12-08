---
title: KSPROPERTY \_ 连接 \_ 优先级
description: 客户端使用 KSPROPERTY \_ 连接 \_ 优先级属性来获取或设置连接的优先级。
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
ms.openlocfilehash: 56e88efd74ef65ef13faa2e27f1b5cef416a962e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786631"
---
# <a name="ksproperty_connection_priority"></a>KSPROPERTY \_ 连接 \_ 优先级


客户端使用 KSPROPERTY \_ 连接 \_ 优先级属性来获取或设置连接的优先级。

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
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kspriority" data-raw-source="[&lt;strong&gt;KSPRIORITY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kspriority)"><strong>KSPRIORITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回包含优先级类和子类的 [**KSPRIORITY**](/windows-hardware/drivers/ddi/ks/ns-ks-kspriority) 类型的结构。

如果 **PriorityClass** 成员较大，或 **PriorityClass** 成员完全相同且 **PrioritySubClass** 成员较大，则优先级比另一个优先级大。

以下预定义的 **PriorityClass** 值可用： KSPRIORITY \_ LOW、KSPRIORITY \_ NORMAL、KSPRIORITY \_ HIGH 和 KSPRIORITY \_ EXCLUSIVE。 优先级默认为 KSPRIORITY \_ NORMAL。 KSPRIORITY \_ exclusive 指示连接对 pin 使用的资源具有独占访问权限。

优先级值具有全局重要性：客户端可以使用报告的值在两个不相关的内核流式处理过滤器上设置两个不同的 pin 之间的优先级。

KSPROPERTY \_ 连接 \_ 优先级是可选的。 客户端将不支持该端口的 pin 视为具有优先级 KSPRIORITY \_ NORMAL。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPRIORITY**](/windows-hardware/drivers/ddi/ks/ns-ks-kspriority)

[**KSPIN \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)


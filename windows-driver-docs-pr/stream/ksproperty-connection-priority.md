---
title: KSPROPERTY\_连接\_优先级
description: 客户端使用 KSPROPERTY\_连接\_优先级属性来获取或设置连接的优先级。
ms.assetid: 2037fe95-e176-4714-ad36-65a0e25b29e0
keywords:
- KSPROPERTY_CONNECTION_PRIORITY 流式处理媒体设备
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
ms.openlocfilehash: b190e1f2e7ca88ad5139521b8ddd59f9df3716cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368681"
---
# <a name="kspropertyconnectionpriority"></a>KSPROPERTY\_连接\_优先级


客户端使用 KSPROPERTY\_连接\_优先级属性来获取或设置连接的优先级。

## <span id="ddk_ksproperty_connection_priority_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_PRIORITY_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564250" data-raw-source="[&lt;strong&gt;KSPRIORITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564250)"><strong>KSPRIORITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回类型的结构[ **KSPRIORITY** ](https://msdn.microsoft.com/library/windows/hardware/ff564250) ，其中包含优先级类和子类。

一个优先级大于另一个 if **PriorityClass**成员是更高版本，或者如果**PriorityClass**成员是完全相同并且**PrioritySubClass**成员是更高版本。

以下预定义的值**PriorityClass**可用：KSPRIORITY\_低、 KSPRIORITY\_NORMAL、 KSPRIORITY\_HIGH 和 KSPRIORITY\_排他。 优先级默认值为 KSPRIORITY\_正常。 KSPRIORITY\_排他表示连接中有使用 pin 资源的独占访问权限。

优先级值具有全局意义： 客户端可以使用报告的值设置两个不相关的内核流式处理筛选器在两个不同的 pin 之间的优先级。

KSPROPERTY\_连接\_优先级是可选的。 客户端将不支持它为具有优先级 KSPRIORITY pin\_正常。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPRIORITY**](https://msdn.microsoft.com/library/windows/hardware/ff564250)

[**KSPIN\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff563531)

 

 







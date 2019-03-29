---
title: KSPROPERTY\_CROSSBAR\_ROUTE
description: KSPROPERTY\_纵横制\_ROUTE 属性查询可能特定路由是否和路由通过指定输出插针索引和输入插针索引视频或音频流。 必须实现此属性。
ms.assetid: 2c64575c-49c6-437b-924e-042ee0f15d9b
keywords:
- KSPROPERTY_CROSSBAR_ROUTE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CROSSBAR_ROUTE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e56749a9cacf713128189b15603e97b6b3e6fba1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575834"
---
# <a name="kspropertycrossbarroute"></a>KSPROPERTY\_CROSSBAR\_ROUTE


KSPROPERTY\_纵横制\_ROUTE 属性查询可能特定路由是否和路由通过指定输出插针索引和输入插针索引视频或音频流。 必须实现此属性。

## <span id="ddk_ksproperty_crossbar_route_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_ROUTE_KS"></span>


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
<td><p>Filter</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565128" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565128)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565128" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565128)"><strong>KSPROPERTY_CROSSBAR_ROUTE_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_跨\_路由\_S 结构，用于指定特定的路由和是使用该路由。

<a name="remarks"></a>备注
-------

音频输出插针时传送给输入插针索引-1，应将静音输出音频流，例如何时更改通道。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CROSSBAR\_ROUTE\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565128)

 

 







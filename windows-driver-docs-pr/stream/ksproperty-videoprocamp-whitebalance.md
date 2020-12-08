---
title: KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE
description: KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE 属性设置或获取照相机的白平衡设置。 此属性是可选的。
keywords:
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca6198601b420b9910e509e0777b90f25cb9f5e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840237"
---
# <a name="ksproperty_videoprocamp_whitebalance"></a>KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE


KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE 属性设置或获取照相机的白平衡设置。 此属性是可选的。

## <span id="ddk_ksproperty_videoprocamp_whitebalance_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_KS"></span>


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
<td><p>筛选器或节点</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong></a>或<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是指定相机白平衡设置的 LONG 值。 白平衡值表示为色温度的色温。

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ VIDEOPROCAMP S 结构的 Value 成员 \_ 指定了白平衡设置。

白平衡的范围和默认值取决于设备。 每个视频捕获微型驱动程序都必须为此属性定义一个范围和默认值。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEOPROCAMP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)


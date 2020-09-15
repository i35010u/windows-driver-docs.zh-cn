---
title: KSPROPERTY \_ VIDEOPROCAMP \_ 对比度
description: KSPROPERTY \_ VIDEOPROCAMP \_ 对比度属性控制相机 (亮度增益) 设置。 此属性是可选的。
ms.assetid: 0e94aec4-b258-44be-aa6e-f0a40b803564
keywords:
- KSPROPERTY_VIDEOPROCAMP_CONTRAST 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_CONTRAST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b82426a017346cca6cdfe70e97574b77692d548f
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103006"
---
# <a name="ksproperty_videoprocamp_contrast"></a>KSPROPERTY \_ VIDEOPROCAMP \_ 对比度


KSPROPERTY \_ VIDEOPROCAMP \_ 对比度属性控制相机 (亮度增益) 设置。 此属性是可选的。

## <span id="ddk_ksproperty_videoprocamp_contrast_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_CONTRAST_KS"></span>


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

 

 (操作数据) 的属性值是指定相机对比度设置的 LONG 值。 对比度值表示为增益系数乘以100。

<a name="remarks"></a>注解
-------

KSPROPERTY **Value** \_ VIDEOPROCAMP S 结构的 Value 成员 \_ 指定对比度值。

每个视频捕获微型驱动程序都必须为此属性的 **value** 成员定义一个范围和默认值。 所需范围必须是0到10000。 默认值必须为 100 (1x) 。

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


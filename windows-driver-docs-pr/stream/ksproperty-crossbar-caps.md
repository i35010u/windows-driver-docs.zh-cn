---
title: KSPROPERTY \_ 横线 \_ 帽
description: "\"KSPROPERTY\" \\_ 纵横制 \\_ 下沉属性检索设备上的横线功能 (纵横比) 上的输入和输出插针的数目。 必须实现此属性。"
ms.assetid: f7dd806c-065d-48c7-ab58-3f5ef95451d5
keywords:
- KSPROPERTY_CROSSBAR_CAPS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CROSSBAR_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d0e3e56d11a0afd9544f4ff0bfb45722ef37c60
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102720"
---
# <a name="ksproperty_crossbar_caps"></a>KSPROPERTY \_ 横线 \_ 帽


"KSPROPERTY" \_ 纵横制 \_ 下沉属性检索设备上的横线功能 (纵横比) 上的输入和输出插针的数目。 必须实现此属性。

## <span id="ddk_ksproperty_crossbar_caps_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_CAPS_KS"></span>


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
<td><p>否</p></td>
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_caps_s)"><strong>KSPROPERTY_CROSSBAR_CAPS_S</strong></a></p></td>
<td><p>一对 ULONGs</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一对指定了横线上的音频和视频输入插针数量的 ULONGs，以及多条上的音频和视频输出插针的数目。

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

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ 横线 \_ 大写字母 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_caps_s)


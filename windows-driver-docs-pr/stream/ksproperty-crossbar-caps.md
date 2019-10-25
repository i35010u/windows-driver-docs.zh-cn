---
title: KSPROPERTY\_纵横\_帽
description: KSPROPERTY\_纵横制\_CAP 属性检索设备的横线功能（纵横比的输入插针和输出插针的数目）。 必须实现此属性。
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
ms.openlocfilehash: a11561d6eec827f892b31451ed5a2f2447b8ed51
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844314"
---
# <a name="ksproperty_crossbar_caps"></a>KSPROPERTY\_纵横\_帽


KSPROPERTY\_纵横制\_CAP 属性检索设备的横线功能（纵横比的输入插针和输出插针的数目）。 必须实现此属性。

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
<td><p>无</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_caps_s)"><strong>KSPROPERTY_CROSSBAR_CAPS_S</strong></a></p></td>
<td><p>一对 ULONGs</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一对 ULONGs，它指定了横线上的音频和视频输入插针的数目，以及在横线上的音频和视频输出插针的数目。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_纵横\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_caps_s)

 

 







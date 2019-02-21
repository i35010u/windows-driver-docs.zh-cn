---
title: KSPROPERTY\_CROSSBAR\_CAPS
description: KSPROPERTY\_纵横制\_CAPS 属性检索的设备 （输入和输出插针上纵横制数） 纵横制功能。 必须实现此属性。
ms.assetid: f7dd806c-065d-48c7-ab58-3f5ef95451d5
keywords:
- KSPROPERTY_CROSSBAR_CAPS 流式处理媒体设备
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
ms.openlocfilehash: a78ddd12b15bb56efb6207bee26e218144027ab3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534136"
---
# <a name="kspropertycrossbarcaps"></a>KSPROPERTY\_CROSSBAR\_CAPS


KSPROPERTY\_纵横制\_CAPS 属性检索的设备 （输入和输出插针上纵横制数） 纵横制功能。 必须实现此属性。

## <span id="ddk_ksproperty_crossbar_caps_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_CAPS_KS"></span>


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
<td><p>否</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565120" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565120)"><strong>KSPROPERTY_CROSSBAR_CAPS_S</strong></a></p></td>
<td><p>对的 ULONGs</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一对指定的音频和视频输入插针上横线的 ULONGs 和音频和视频输出插针上纵横制数。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CROSSBAR\_CAPS\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565120)

 

 







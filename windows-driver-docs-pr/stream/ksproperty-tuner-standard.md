---
title: KSPROPERTY\_调谐器\_标准
description: KSPROPERTY\_调谐器\_标准属性检索当前的模拟视频标准。 必须实现此属性。
ms.assetid: b20dd01c-bd6b-4908-a3c4-eb2914eb54d0
keywords:
- KSPROPERTY_TUNER_STANDARD 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_STANDARD
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78f1b26e286856f17d68145e0920b2eb371b8d86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837900"
---
# <a name="ksproperty_tuner_standard"></a>KSPROPERTY\_调谐器\_标准


KSPROPERTY\_调谐器\_标准属性检索当前的模拟视频标准。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_standard_ks"></span><span id="DDK_KSPROPERTY_TUNER_STANDARD_KS"></span>


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
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s)"><strong>KSPROPERTY_TUNER_STANDARD_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，指定调谐器的优化标准。

<a name="remarks"></a>备注
-------

KSPROPERTY\_调谐器\_标准\_S 结构的**标准**成员指定了当前的模拟视频标准。

仅当当前模式\_调谐器\_模式\_TV 时，才使用此属性。

可以按照多种不同的模拟电视标准（例如 NTSC、PAL 或 SECAM）来广播模拟电视信号。 客户端使用 KSPROPERTY\_调谐器\_模式\_CAP 属性来查询支持的标准，并使用 KSPROPERTY\_调谐器\_STANDARD 获取或设置电视调谐器设备的当前标准。

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

[**KSPROPERTY\_调谐器\_标准\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_s)

[**KSPROPERTY\_调谐器\_模式**](ksproperty-tuner-mode.md)

 

 







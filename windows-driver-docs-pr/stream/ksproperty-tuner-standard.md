---
title: KSPROPERTY\_调谐器\_标准
description: KSPROPERTY\_调谐器\_标准属性检索当前的模拟视频标准。 必须实现此属性。
ms.assetid: b20dd01c-bd6b-4908-a3c4-eb2914eb54d0
keywords:
- KSPROPERTY_TUNER_STANDARD 流式处理媒体设备
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
ms.openlocfilehash: 714f3aaa748f99d3145d963338d43a207ede8cf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342145"
---
# <a name="kspropertytunerstandard"></a>KSPROPERTY\_调谐器\_标准


KSPROPERTY\_调谐器\_标准属性检索当前的模拟视频标准。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_standard_ks"></span><span id="DDK_KSPROPERTY_TUNER_STANDARD_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565918" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565918)"><strong>KSPROPERTY_TUNER_STANDARD_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 ULONG，指定该调谐器的优化标准。

<a name="remarks"></a>备注
-------

**标准**KSPROPERTY 成员\_调谐器\_标准\_S 结构指定的当前模拟视频标准。

使用此属性仅当当前模式为 KSPROPERTY\_调谐器\_模式\_电视。

可以根据多个不同模拟电视标准如 NTSC、 PAL 或 SECAM 广播模拟电视信号。 客户端使用 KSPROPERTY\_调谐器\_模式\_CAPS 属性，可以查询支持的标准，并且使用 KSPROPERTY\_调谐器\_标准要获取或设置当前标准电视调谐器设备。

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

[**KSPROPERTY\_调谐器\_标准\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565918)

[**KSPROPERTY\_调谐器\_模式**](ksproperty-tuner-mode.md)

 

 







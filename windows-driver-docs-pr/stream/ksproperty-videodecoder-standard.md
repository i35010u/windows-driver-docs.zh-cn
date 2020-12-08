---
title: KSPROPERTY \_ VIDEODECODER \_ 标准
description: KSPROPERTY \_ VIDEODECODER \_ standard 属性控制当前的模拟视频标准。 必须实现此属性。
keywords:
- KSPROPERTY_VIDEODECODER_STANDARD 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_STANDARD
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f72e7e9fdcb604fc24d19271c3c3f3a892e702b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840859"
---
# <a name="ksproperty_videodecoder_standard"></a>KSPROPERTY \_ VIDEODECODER \_ 标准


KSPROPERTY \_ VIDEODECODER \_ standard 属性控制当前的模拟视频标准。 必须实现此属性。

## <span id="ddk_ksproperty_videodecoder_standard_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_STANDARD_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是指定当前模拟视频标准的 ULONG。

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ VIDEODECODER S 结构的 Value 成员 \_ 指定当前的模拟视频标准。

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

[**KSPROPERTY \_ VIDEODECODER \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)


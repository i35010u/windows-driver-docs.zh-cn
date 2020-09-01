---
title: KSPROPERTY \_ VIDEODECODER \_ 标准
description: KSPROPERTY \_ VIDEODECODER \_ standard 属性控制当前的模拟视频标准。 必须实现此属性。
ms.assetid: 955c267a-703e-4d18-a4e9-710f316cfb48
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
ms.openlocfilehash: cd6e8a0eb5305a8d3af8505c85b3cb645ae375a5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189941"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
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

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEODECODER \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)

 


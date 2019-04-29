---
title: KSPROPERTY\_VIDEODECODER\_输出\_启用
description: KSPROPERTY\_VIDEODECODER\_输出\_启用属性控制驻留在共享的视频端口总线的视频解码器的三种状态输出。 此属性为可选项。
ms.assetid: 33c9a3d2-ffc0-4460-abc4-56bc83c64b55
keywords:
- KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b8d86f384112e86446b9223543b765e5431644d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325985"
---
# <a name="kspropertyvideodecoderoutputenable"></a>KSPROPERTY\_VIDEODECODER\_输出\_启用


KSPROPERTY\_VIDEODECODER\_输出\_启用属性控制驻留在共享的视频端口总线的视频解码器的三种状态输出。 此属性为可选项。

## <span id="ddk_ksproperty_videodecoder_output_enable_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566052" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566052)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为的 ULONG 的指定设置的允许三种状态输出。 值为零表示三种状态输出。 一个非零值指示设备正在主动推动的视频端口总线。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEODECODER\_S 结构指定的三个输出启用设置。

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

[**KSPROPERTY\_VIDEODECODER\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566052)

 

 







---
title: KSPROPERTY \_ 流 \_ FRAMETIME
description: KSPROPERTY \_ STREAM \_ FRAMETIME 属性允许客户端根据特定的媒体流确定下一个帧的持续时间，并使用该信息来逐步处理序列。
ms.assetid: 0cc218eb-1f21-4b45-ac48-b3e308bddfaf
keywords:
- KSPROPERTY_STREAM_FRAMETIME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_FRAMETIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd83e94f8049fbb05e1214a482bb22722d6f2ad4
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103028"
---
# <a name="ksproperty_stream_frametime"></a>KSPROPERTY \_ 流 \_ FRAMETIME


KSPROPERTY \_ STREAM \_ FRAMETIME 属性允许客户端根据特定的媒体流确定下一个帧的持续时间，并使用该信息来逐步处理序列。

## <span id="ddk_ksproperty_stream_frametime_ks"></span><span id="DDK_KSPROPERTY_STREAM_FRAMETIME_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksframetime" data-raw-source="[&lt;strong&gt;KSFRAMETIME&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksframetime)"><strong>KSFRAMETIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY \_ STREAM \_ FRAMETIME 是一个可选属性，如果 pin 识别出正在传输的媒体类型的细节，则应该实现该属性。

此属性受呈现插针支持，并用于返回下一帧数据的持续时间以及与该帧关联的任何标志。 帧通常是可以拆分数据的最小可用单元。 对于视频流，这可能是一个视频帧或一个字段。 对于音频，这是流中每个通道的示例。 对于 MIDI，这将是下一个 MIDI 事件。

持续时间是根据 pin 提供的显示时间单位来度量。 这取决于显示时间中使用的接口和分子/分母对。 这不适用于不面向任何特定媒体类型（例如一般文件读取器）的流。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSFRAMETIME**](/windows-hardware/drivers/ddi/ks/ns-ks-ksframetime)


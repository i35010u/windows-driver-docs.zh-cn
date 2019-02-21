---
title: KSPROPERTY\_STREAM\_FRAMETIME
description: KSPROPERTY\_流\_FRAMETIME 属性允许客户端确定基于特定媒体流的下一个帧的持续时间，并使用该信息到步骤帧序列。
ms.assetid: 0cc218eb-1f21-4b45-ac48-b3e308bddfaf
keywords:
- KSPROPERTY_STREAM_FRAMETIME 流式处理媒体设备
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
ms.openlocfilehash: e58877f78599834bd2e874ce1d05df3dea3cdd6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541318"
---
# <a name="kspropertystreamframetime"></a>KSPROPERTY\_STREAM\_FRAMETIME


KSPROPERTY\_流\_FRAMETIME 属性允许客户端确定基于特定媒体流的下一个帧的持续时间，并使用该信息到步骤帧序列。

## <span id="ddk_ksproperty_stream_frametime_ks"></span><span id="DDK_KSPROPERTY_STREAM_FRAMETIME_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562558" data-raw-source="[&lt;strong&gt;KSFRAMETIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562558)"><strong>KSFRAMETIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_流\_FRAMETIME 是如果 pin 识别出它传输的媒体类型的具体情况应实现的可选属性。

该属性支持的呈现插针，用于返回下一个帧的数据以及与该框架相关联的所有标志的持续时间。 框架通常是可使用最小的单元的数据可以拆分。 对于视频流，这可能是视频帧或字段。 对于音频，这将是用于在流中每个通道的示例。 对于 MIDI，这将是下一步的 MIDI 事件。

持续时间单位根据提供的 pin 的演示文稿时间单位。 这是依赖于该接口和分子/分母对中的呈现时间使用。 这不适用于不是针对任何特定的媒体类型，如通用文件读取的流。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSFRAMETIME**](https://msdn.microsoft.com/library/windows/hardware/ff562558)

 

 







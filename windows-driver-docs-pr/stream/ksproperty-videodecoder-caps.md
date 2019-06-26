---
title: KSPROPERTY\_VIDEODECODER\_CAP
description: KSPROPERTY\_VIDEODECODER\_CAPS 属性描述视频解码器的基本功能。 必须实现此属性。
ms.assetid: 8b252f36-911b-4f51-894d-3aae9aa9dfde
keywords:
- KSPROPERTY_VIDEODECODER_CAPS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5466109a8f4dcd43c0289811bb7d0b5d3f63ca17
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382010"
---
# <a name="kspropertyvideodecodercaps"></a>KSPROPERTY\_VIDEODECODER\_CAP


KSPROPERTY\_VIDEODECODER\_CAPS 属性描述视频解码器的基本功能。 必须实现此属性。

## <span id="ddk_ksproperty_videodecoder_caps_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_CAPS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s)"><strong>KSPROPERTY_VIDEODECODER_CAPS_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s)"><strong>KSPROPERTY_VIDEODECODER_CAPS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_VIDEODECODER\_CAPS\_S 结构，如指定视频解码器设备的硬件功能支持的标准，确定时间和水平同步的波视频解码器在垂直同步期间生成。

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

[**KSPROPERTY\_VIDEODECODER\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s)

 

 







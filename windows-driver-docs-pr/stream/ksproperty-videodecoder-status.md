---
title: KSPROPERTY\_VIDEODECODER\_状态
description: KSPROPERTY\_VIDEDECODER\_STATUS 属性从视频解码器中检索状态信息。 必须实现此属性。
ms.assetid: 1d8cb537-1d85-4536-bd75-33beea0f586d
keywords:
- KSPROPERTY_VIDEODECODER_STATUS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86a5af3f2f3f3d2244e1eb444bb49e18115b44cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381988"
---
# <a name="kspropertyvideodecoderstatus"></a>KSPROPERTY\_VIDEODECODER\_状态


KSPROPERTY\_VIDEDECODER\_STATUS 属性从视频解码器中检索状态信息。 必须实现此属性。

## <span id="ddk_ksproperty_videodecoder_status_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_STATUS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_VIDEODECODER\_状态\_S 结构，它指定视频解码设备，例如传入模拟信号中的行数的存在状态和是否锁定信号。

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

[**KSPROPERTY\_VIDEODECODER\_状态\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s)

 

 







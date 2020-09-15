---
title: KSPROPERTY \_ VIDEODECODER \_ 状态
description: KSPROPERTY \_ VIDEDECODER \_ STATUS 属性从视频解码器检索状态信息。 必须实现此属性。
ms.assetid: 1d8cb537-1d85-4536-bd75-33beea0f586d
keywords:
- KSPROPERTY_VIDEODECODER_STATUS 流媒体设备
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
ms.openlocfilehash: 5ccdf23cb16e352f486bb81c2846c80efdeef147
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103536"
---
# <a name="ksproperty_videodecoder_status"></a>KSPROPERTY \_ VIDEODECODER \_ 状态


KSPROPERTY \_ VIDEDECODER \_ STATUS 属性从视频解码器检索状态信息。 必须实现此属性。

## <span id="ddk_ksproperty_videodecoder_status_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_STATUS_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ VIDEODECODER \_ 状态 \_ S 结构，该结构指定视频解码设备的当前状态，例如传入模拟信号中的行数，以及信号是否已锁定。

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

[**KSPROPERTY \_ VIDEODECODER \_ 状态 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s)


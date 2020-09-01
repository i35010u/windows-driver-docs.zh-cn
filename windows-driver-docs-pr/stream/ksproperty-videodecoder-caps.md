---
title: KSPROPERTY \_ VIDEODECODER \_ CAP
description: KSPROPERTY \_ VIDEODECODER \_ cap 属性描述视频解码器的基本功能。 必须实现此属性。
ms.assetid: 8b252f36-911b-4f51-894d-3aae9aa9dfde
keywords:
- KSPROPERTY_VIDEODECODER_CAPS 流媒体设备
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
ms.openlocfilehash: 05c445540714b58d5fe6012982f2f0ae7f71afdb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189949"
---
# <a name="ksproperty_videodecoder_caps"></a>KSPROPERTY \_ VIDEODECODER \_ CAP


KSPROPERTY \_ VIDEODECODER \_ cap 属性描述视频解码器的基本功能。 必须实现此属性。

## <span id="ddk_ksproperty_videodecoder_caps_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_CAPS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s)"><strong>KSPROPERTY_VIDEODECODER_CAPS_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s)"><strong>KSPROPERTY_VIDEODECODER_CAPS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ VIDEODECODER \_ cap \_ S 结构，它指定视频解码器设备的硬件功能，例如支持的标准、结算时间和视频解码器在垂直同步期间生成的水平同步脉冲。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEODECODER \_ CAP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s)

 


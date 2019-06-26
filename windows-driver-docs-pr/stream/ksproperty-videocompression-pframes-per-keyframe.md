---
title: KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_每\_关键帧
description: KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_每\_关键帧属性控制预测的帧 （P 帧） 间隔。 必须实现此属性。
ms.assetid: feb839b4-32fc-4fe9-b015-019d9d683c66
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b5fe3265cb7a2369b6568a8b0de106e3ca1e49e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382024"
---
# <a name="kspropertyvideocompressionpframesperkeyframe"></a>KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_每\_关键帧


KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_每\_关键帧属性控制预测的帧 （P 帧） 间隔。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_pframes_per_keyframe_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME_KS"></span>


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
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 long 类型的值，用于指定预测每个关键帧的帧数。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEOCOMPRESSION\_S 结构指定每个关键帧的 P 帧数。 如果 set 请求提供了一个否定**值**，微型驱动程序应将 P 帧速率设置为默认值。

微型驱动程序支持此属性应设置 KS\_VideoCompressionCaps\_CanBFrame 标志**功能**的成员[ **KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)检索微型驱动程序的视频的压缩功能的结构。

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

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 

 







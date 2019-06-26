---
title: KSPROPERTY\_音频\_宽度
description: KSPROPERTY\_音频\_宽度属性指定的立体声图像的宽度 （明显宽度）。
ms.assetid: 56b18337-c29b-437f-b52f-8d804d857729
keywords:
- KSPROPERTY_AUDIO_WIDENESS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_WIDENESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39139a500d9ccdceb437d03d4e9e31ab40f001af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360578"
---
# <a name="kspropertyaudiowideness"></a>KSPROPERTY\_音频\_宽度


KSPROPERTY\_音频\_宽度属性指定的立体声图像的宽度 （明显宽度）。

## <span id="ddk_ksproperty_audio_wideness_ks"></span><span id="DDK_KSPROPERTY_AUDIO_WIDENESS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是类型为 ULONG，它指定宽度。 宽度表示为一个 16 位小数的无符号的定点值。 宽度值从 0 到 0xFFFFFFFF 遵循线性范围：

-   值 0x00010000 表示 unity （100%)，指示与帧的左右扬声器的区域中应保持一致立体声图像的宽度。

-   对于值大于 unity，立体声映像应出现的左右扬声器设计框架的区域外扩展。

-   值小于 unity，感知立体声图像的宽度应小于左右扬声器之间的空间。

-   零值指示声音应显示为来自正好左右扬声器位置。

明显立体声图像的宽度应以线性方式增加宽度值中的线性增加。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_宽度属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

这是宽度节点的属性 ([**KSNODETYPE\_立体声\_宽**](ksnodetype-stereo-wide.md))。 宽度节点可以将 spaciousness 添加到现有的立体声 （两个通道） 流。 若要实现此效果，节点处理的流，以使某些听起来似乎源自的左右扬声器包含在区域之外的位置。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_立体声\_宽**](ksnodetype-stereo-wide.md)

 

 







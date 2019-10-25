---
title: KSPROPERTY\_音频\_CHORUS\_级别
description: KSPROPERTY\_音频\_CHORUS\_LEVEL 属性指定 CHORUS 级别。 这是 chorus 节点的属性（KSNODETYPE\_CHORUS）。
ms.assetid: 80541b2c-0fb3-4306-8ed2-e524b5a4c113
keywords:
- KSPROPERTY_AUDIO_CHORUS_LEVEL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHORUS_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e489ea8cdce5f994827e4ae5d9fdf862eac3f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831061"
---
# <a name="ksproperty_audio_chorus_level"></a>KSPROPERTY\_音频\_CHORUS\_级别


KSPROPERTY\_音频\_CHORUS\_LEVEL 属性指定 CHORUS 级别。 这是 chorus 节点的属性（[**KSNODETYPE\_chorus**](ksnodetype-chorus.md)）。

## <span id="ddk_ksproperty_audio_chorus_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CHORUS_LEVEL_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 ULONG，并指定 chorus 级别。 Chorus 级别值后跟0到 100\*（65536-1/65536）% 之间的线性范围：

-   值0x00010000 表示100%。

-   值0xFFFFFFFF 表示 100\*（65536-1/65536）%。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_CHORUS\_级别属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于获取和设置 chorus 回显的音量级别。

Chorus 是一种通过回显原始声音来创建的音频线效果，稍微延迟，稍微 modulating 回声的延迟。 有关详细信息，请参阅 Microsoft Windows SDK 文档中的**IDirectSoundFXChorus**接口的说明。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE\_CHORUS**](ksnodetype-chorus.md)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

 

 







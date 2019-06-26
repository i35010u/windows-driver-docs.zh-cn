---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE 属性指定的三维声音缓冲区的最小距离。
ms.assetid: 998e591d-7c23-4857-908c-4e90918c9a94
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71fe5a550bdea609cfd1b14fbf1b28875cc2026c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358803"
---
# <a name="kspropertydirectsound3dbuffermindistance"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE


KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE 属性指定的三维声音缓冲区的最小距离。

## <span id="ddk_ksproperty_directsound3dbuffer_mindistance_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>浮点数</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值类型为 FLOAT 的是，它指定的最小距离。 距离单位的信息，请参阅[ **KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

在的距离小于声音源中的最小距离，声音的音量不再提高随着距离的降低。 DirectSound 3D 缓冲区的最小距离有关的详细信息，请参阅 Microsoft Windows SDK 文档中的以下：

-   **FlMinDistance** DS3DBUFFER 结构中的成员。

-   **IDirectSound3DBuffer::GetMinDistance**并**IDirectSound3DBuffer::SetMinDistance**方法。

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

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

 

 







---
title: KSPROPERTY\_VIDEOCOMPRESSION\_质量
description: KSPROPERTY\_VIDECOMPRESSION\_质量属性控制视频的压缩质量设置。 必须实现此属性。
ms.assetid: 7566f60e-fe49-4009-bd61-b29d2adb4e8c
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_QUALITY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_QUALITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39f1e1e8f4f2a4ed9ba8cd650eb9cb479172e4b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360835"
---
# <a name="kspropertyvideocompressionquality"></a>KSPROPERTY\_VIDEOCOMPRESSION\_质量


KSPROPERTY\_VIDECOMPRESSION\_质量属性控制视频的压缩质量设置。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_quality_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_QUALITY_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566018" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566018)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 long 类型的值，指定视频的压缩质量值。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEOCOMPRESSION\_S 结构指定质量度量值。

此属性范围为从 0 到 10000 的值。 零表示最低质量，10000 最高。 微型驱动程序确定自己的默认值。

微型驱动程序支持此属性应设置**KS\_CompressionCaps\_CanQuality**标记中**功能**隶属[ **KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565979)检索微型驱动程序的视频的压缩功能的结构。 如果微型驱动程序设置 KS\_CompressionCaps\_CanQuality，它应支持这两个 get 和 set 属性的请求。

此属性范围为从 0 到 10000 的值。 零表示最低质量，10000 最高。 微型驱动程序确定自己的默认值。

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

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566018)

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565979)

 

 







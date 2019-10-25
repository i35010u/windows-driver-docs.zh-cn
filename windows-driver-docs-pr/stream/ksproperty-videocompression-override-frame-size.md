---
title: KSPROPERTY\_VIDEOCOMPRESSION\_覆盖\_帧\_大小
description: KSPROPERTY\_VIDEOCOMPRESSION\_覆盖\_帧\_大小属性将暂时覆盖帧大小（字节数）。 此属性为可选项。
ms.assetid: 626b0dcf-3087-407b-8e7f-00314de7d2f2
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f99b3c60addd91d742a04f1c635392592b9e07e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837886"
---
# <a name="ksproperty_videocompression_override_frame_size"></a>KSPROPERTY\_VIDEOCOMPRESSION\_覆盖\_帧\_大小


KSPROPERTY\_VIDEOCOMPRESSION\_覆盖\_帧\_大小属性将暂时覆盖帧大小（字节数）。 此属性为可选项。

## <span id="ddk_ksproperty_videocompression_override_frame_size_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE_KS"></span>


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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定临时帧大小替代值的 LONG。

<a name="remarks"></a>备注
-------

KSPROPERTY\_VIDEOCOMPRESSION\_S 结构的**值**成员指定帧的覆盖数据速率。

支持此属性的微型驱动程序应将**KS\_CompressionCaps\_CanCrunch**标志设置为[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)结构的**功能**成员，检索设备的视频压缩功能。

视频捕获微型驱动程序不支持此属性。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 

 







---
title: KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 帧 \_ 大小
description: KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 帧 \_ 大小属性暂时覆盖帧大小 (字节计数) 。 此属性是可选的。
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
ms.openlocfilehash: e25377dcc21904d77570d96b4d9141ac351e1970
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185869"
---
# <a name="ksproperty_videocompression_override_frame_size"></a>KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 帧 \_ 大小


KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 帧 \_ 大小属性暂时覆盖帧大小 (字节计数) 。 此属性是可选的。

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
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是指定临时帧大小替代值的 LONG。

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ VIDEOCOMPRESSION S 结构的值成员 \_ 指定帧的覆盖数据速率。

支持此属性的微型驱动程序应将**KS \_ CompressionCaps \_ CanCrunch**标志设置为[**KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)结构的**功能**成员，该成员检索设备的视频压缩功能。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 


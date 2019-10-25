---
title: KSPROPERTY\_VIDEOCOMPRESSION\_WINDOWSIZE
description: KSPROPERTY\_VIDEOCOMPRESSION\_WINDOWSIZE 属性控制描述平均帧大小的数据速率。 必须实现此属性。
ms.assetid: 44cf4bb6-7ddb-4a72-8a77-7dc390aa8c12
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b2d2fd8ad29c110c73ee9240b8ed2600b92caa2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837878"
---
# <a name="ksproperty_videocompression_windowsize"></a>KSPROPERTY\_VIDEOCOMPRESSION\_WINDOWSIZE


KSPROPERTY\_VIDEOCOMPRESSION\_WINDOWSIZE 属性控制描述平均帧大小的数据速率。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_windowsize_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE_KS"></span>


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
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定表示平均帧大小的数据速率的 LONG。

<a name="remarks"></a>备注
-------

KSPROPERTY\_VIDEOCOMPRESSION\_S 结构的**值**成员指定窗口大小。

支持此属性的微型驱动程序应将**KS\_CompressionCaps\_CanWindow**标志设置为[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)结构的**功能**成员，检索微型驱动程序的视频压缩功能。 如果微型驱动程序将**KS\_CompressionCaps 设置\_CanWindow**标志，则它应同时提供对属性的 get 和 set 支持。

对于大小为 n 的窗口 *，* 任何连续*n*帧的平均帧大小不得超过流的指定数据速率，尽管*各个*帧可能更大或更小。 例如，如果已将每秒15帧（fps）电影的数据速率设置为每秒 150 kb，则每个帧的*平均*大小必须小于或等于 10 kb。 只要平均大小（每秒15帧的大小计算）小于或等于 10 kb，单独帧就可能更大或更小。

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

 

 







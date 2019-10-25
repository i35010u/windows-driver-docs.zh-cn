---
title: KSPROPERTY\_VIDEOCONTROL\_帧\_速率
description: KSPROPERTY\_VIDEOCONTROL\_帧\_率属性枚举可用的帧速率。 此属性为可选项。
ms.assetid: f2b6fabc-c03b-4fa5-9e5b-43d7a1c26578
keywords:
- KSPROPERTY_VIDEOCONTROL_FRAME_RATES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_FRAME_RATES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 319d5dec3856aadd69eef5ae84d78a495737e503
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837874"
---
# <a name="ksproperty_videocontrol_frame_rates"></a>KSPROPERTY\_VIDEOCONTROL\_帧\_速率


KSPROPERTY\_VIDEOCONTROL\_帧\_率属性枚举可用的帧速率。 此属性为可选项。

## <span id="ddk_ksproperty_videocontrol_frame_rates_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_FRAME_RATES_KS"></span>


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
<td><p>无</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>数组</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 KSMULTIPLE\_项数组，描述以100毫微秒为单位的可用帧速率。

<a name="remarks"></a>备注
-------

可用帧速率在 KSMULTIPLE\_项数组中返回。 应用程序会将微型驱动程序 KSPROPERTY\_VIDEOCONTROL\_帧\_速率请求，指定 KSPROPERTY 中的流索引和图像维度\_VIDEOCONTROL\_S 结构\_帧\_速率。 微型驱动程序返回调用方的 KSMULTIPLE\_项数组缓冲区中的帧速率信息。 此缓冲区具有固定的标头（KSMULTIPLE\_项）和后面的可变长度数据量（基于 KSMULTIPLE\_项结构中的值）。

单个值为 100-nansecond 增量。

如果传递给微型驱动程序的缓冲区大小为零，则微型驱动程序应将\_请求\_的\_HW 的**NumberOfBytesToTransfer**成员设置为将传递给微型驱动程序的块结构设置为所需的缓冲区大小，返回状态\_缓冲区\_溢出。

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

[**KSPROPERTY\_VIDEOCONTROL\_帧\_速率\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s)

 

 







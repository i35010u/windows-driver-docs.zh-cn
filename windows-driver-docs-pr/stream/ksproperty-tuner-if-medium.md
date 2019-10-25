---
title: KSPROPERTY\_调谐器\_如果\_中型
description: KSPROPERTY\_调谐器\_如果\_中型介绍了支持数字电视调谐的设备的中间频率 pin 的媒介。 此属性为可选项。
ms.assetid: 1144777c-e81c-4b8f-a634-411591c71356
keywords:
- KSPROPERTY_TUNER_IF_MEDIUM 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_IF_MEDIUM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d21ef1f5a5d48c2525c3d4a74b54e447da431b3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837916"
---
# <a name="ksproperty_tuner_if_medium"></a>KSPROPERTY\_调谐器\_如果\_中型


KSPROPERTY\_调谐器\_如果\_中型介绍了支持数字电视调谐的设备的中间频率 pin 的媒介。 此属性为可选项。

## <span id="ddk_ksproperty_tuner_if_medium_ks"></span><span id="DDK_KSPROPERTY_TUNER_IF_MEDIUM_KS"></span>


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
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_if_medium_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_IF_MEDIUM_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_if_medium_s)"><strong>KSPROPERTY_TUNER_IF_MEDIUM_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff563538(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPIN_MEDIUM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))"><strong>KSPIN_MEDIUM</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种 KSPIN\_中型结构，它为能够支持优化到中间频率的 pin 指定中型 GUID。

<a name="remarks"></a>备注
-------

如果\_中型\_结构指定中间频率 pin 的中等 GUID，则\_的 KSPROPERTY\_调谐器的**IFMedium**成员。

如果视频捕获微型驱动程序支持 KSPROPERTY\_调谐器\_如果\_MEDIUM，则*kstvtune.ax*会创建一个附加的 pin，它表示源自调谐器的基于硬件的 mpeg-2 传输流。 此 pin 仅用于定义关系图拓扑。 从*kstvtune.ax*上的此插针流向用户模式流的数据样本包含[**KS\_TVTUNER\_更改\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_tvtuner_change_info)结构。

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

[**如果\_中型\_，则 KSPROPERTY\_调谐器\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_if_medium_s)

 

 







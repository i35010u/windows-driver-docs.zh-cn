---
title: KSPROPERTY\_调谐器\_如果\_介质
description: KSPROPERTY\_调谐器\_如果\_中介绍了中间频率 pin 支持数字电视优化的设备使用的介质。 此属性为可选项。
ms.assetid: 1144777c-e81c-4b8f-a634-411591c71356
keywords:
- KSPROPERTY_TUNER_IF_MEDIUM 流式处理媒体设备
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
ms.openlocfilehash: 445074b364830feb5db04c97448226ba3ff8ad3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355818"
---
# <a name="kspropertytunerifmedium"></a>KSPROPERTY\_调谐器\_如果\_介质


KSPROPERTY\_调谐器\_如果\_中介绍了中间频率 pin 支持数字电视优化的设备使用的介质。 此属性为可选项。

## <span id="ddk_ksproperty_tuner_if_medium_ks"></span><span id="DDK_KSPROPERTY_TUNER_IF_MEDIUM_KS"></span>


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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565848" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_IF_MEDIUM_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565848)"><strong>KSPROPERTY_TUNER_IF_MEDIUM_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563538" data-raw-source="[&lt;strong&gt;KSPIN_MEDIUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563538)"><strong>KSPIN_MEDIUM</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPIN\_中等结构，它指定是否能够支持优化到中间频率 pin 介质 GUID。

<a name="remarks"></a>备注
-------

**IFMedium** KSPROPERTY 成员\_调谐器\_如果\_中等\_S 结构指定的中间频率 pin 介质 GUID。

如果视频捕获微型驱动程序支持 KSPROPERTY\_调谐器\_IF\_介质，然后*kstvtune.ax*创建其他的 pin，表示基于硬件的 mpeg-2 传输流源于调谐器。 此 pin 仅用于定义关系图拓扑。 通过此 pin 的用户模式下流上流动的数据样本*kstvtune.ax*组成[ **KS\_TVTUNER\_更改\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567691)结构。

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

[**KSPROPERTY\_调谐器\_IF\_MEDIUM\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565848)

 

 







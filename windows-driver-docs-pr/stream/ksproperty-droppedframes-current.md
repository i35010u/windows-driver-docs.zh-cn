---
title: KSPROPERTY\_DROPPEDFRAMES\_当前
description: KSPROPERTY\_丢弃\_帧\_已捕获的帧数，丢帧数，数目平均帧大小的 CURRENT 属性中动态检索视频捕获微型驱动程序。 必须实现此属性。
ms.assetid: 43367858-4e3b-476e-aaa5-c9e665df8dc6
keywords:
- KSPROPERTY_DROPPEDFRAMES_CURRENT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DROPPEDFRAMES_CURRENT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f39c780b1c308cd0af5fe093f692f59d08078da7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566145"
---
# <a name="kspropertydroppedframescurrent"></a>KSPROPERTY\_DROPPEDFRAMES\_当前


KSPROPERTY\_丢弃\_帧\_已捕获的帧数，丢帧数，数目平均帧大小的 CURRENT 属性中动态检索视频捕获微型驱动程序。 必须实现此属性。

## <span id="ddk_ksproperty_droppedframes_current_ks"></span><span id="DDK_KSPROPERTY_DROPPEDFRAMES_CURRENT_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565138" data-raw-source="[&lt;strong&gt;KSPROPERTY_DROPPEDFRAMES_CURRENT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565138)"><strong>KSPROPERTY_DROPPEDFRAMES_CURRENT_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565138" data-raw-source="[&lt;strong&gt;KSPROPERTY_DROPPEDFRAMES_CURRENT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565138)"><strong>KSPROPERTY_DROPPEDFRAMES_CURRENT_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_DROPPEDFRAMES\_当前\_S 结构，它指定当前图片数、 丢弃的帧的计数和捕获的帧的平均大小。

<a name="remarks"></a>备注
-------

流状态转换从停止暂停时，应重置捕获帧和丢帧数的计数。

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

[**KSPROPERTY\_DROPPEDFRAMES\_当前\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565138)

 

 







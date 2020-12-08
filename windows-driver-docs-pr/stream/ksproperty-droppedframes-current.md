---
title: KSPROPERTY \_ DROPPEDFRAMES \_ CURRENT
description: "\"KSPROPERTY \\_ 删除 \\_ 帧\" \\_ 当前属性动态检索捕获的帧数、丢弃的帧数和平均帧大小的视频捕获微型驱动程序。 必须实现此属性。"
keywords:
- KSPROPERTY_DROPPEDFRAMES_CURRENT 流媒体设备
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
ms.openlocfilehash: fe9d0d2a942290beb3166e3adb13f065e0c1a29c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795815"
---
# <a name="ksproperty_droppedframes_current"></a>KSPROPERTY \_ DROPPEDFRAMES \_ CURRENT


"KSPROPERTY \_ 删除 \_ 帧" \_ 当前属性动态检索捕获的帧数、丢弃的帧数和平均帧大小的视频捕获微型驱动程序。 必须实现此属性。

## <span id="ddk_ksproperty_droppedframes_current_ks"></span><span id="DDK_KSPROPERTY_DROPPEDFRAMES_CURRENT_KS"></span>


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
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_DROPPEDFRAMES_CURRENT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)"><strong>KSPROPERTY_DROPPEDFRAMES_CURRENT_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_DROPPEDFRAMES_CURRENT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)"><strong>KSPROPERTY_DROPPEDFRAMES_CURRENT_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ DROPPEDFRAMES \_ 当前的 \_ 结构，该结构指定当前的图片号、丢弃的帧的计数以及捕获的帧的平均大小。

<a name="remarks"></a>备注
-------

流状态从停止转换到暂停时，捕获的帧数和丢弃的帧数都应重置。

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

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ DROPPEDFRAMES \_ 当前 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)


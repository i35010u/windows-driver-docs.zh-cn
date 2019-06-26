---
title: KSPROPERTY\_ALLOCATOR\_控制\_面\_大小
description: KSPROPERTY\_ALLOCATOR\_控制\_面\_大小属性会通知客户端筛选器提供 （如覆盖 Mixer) DirectDraw 图面上的分配器捕获操作过程中以及，必须在固定大小，而不考虑在覆盖区上的当前大小分配 Microsoft DirectDraw 图面。 此属性为可选项。
ms.assetid: fc759013-9dd7-44fc-a0d7-fd2585975966
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1b310806e9fac7a9cc10e1012f3b955cb18d804
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386932"
---
# <a name="kspropertyallocatorcontrolsurfacesize"></a>KSPROPERTY\_ALLOCATOR\_控制\_面\_大小


KSPROPERTY\_ALLOCATOR\_控制\_面\_大小属性会通知客户端筛选器提供 （如覆盖 Mixer) DirectDraw 图面上的分配器捕获操作过程中以及，必须在固定大小，而不考虑在覆盖区上的当前大小分配 Microsoft DirectDraw 图面。 此属性为可选项。

## <span id="ddk_ksproperty_allocator_control_surface_size_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_allocator_control_surface_size_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_allocator_control_surface_size_s)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_S</strong></a></p></td>
<td><p>对的 ULONGs</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一对 ULONGs 指定宽度和高度的覆盖面。

<a name="remarks"></a>备注
-------

支持此属性的微型驱动程序返回 KSPROPERTY\_ALLOCATOR\_控制\_面\_大小\_S 结构描述的宽度和高度所需的覆盖面。 覆盖 Mixer 分配此大小的覆盖面。 如果这不是 pin 连接过程中的媒体类型指定的大小，视频会在此大小的视频端口进行缩放。 没有其他在进行缩放的视频端口发生而不考虑 VGA 芯片的缩放功能。

覆盖 Mixer 始终查询此新属性，如果混音器连接到此属性通过其主输入插针上的视频端口上游筛选器。 如果该筛选器未实现此属性，覆盖 Mixer 将假定它不捕获数据并缩放的视频的视频端口，根据需要保留正确显示视频。

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

[**KSPROPERTY\_ALLOCATOR\_控制\_面\_大小\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_allocator_control_surface_size_s)

 

 







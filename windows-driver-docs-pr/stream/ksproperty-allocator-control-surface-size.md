---
title: KSPROPERTY \_ 分配器 \_ 控件 \_ 表面 \_ 大小
description: KSPROPERTY \_ 分配 \_ 器控制 \_ 面 \_ 大小属性通知提供 DirectDraw SURFACE 分配器 (的客户端筛选器，例如覆盖混音) 正在进行捕获操作，并且必须以固定大小分配 Microsoft DirectDraw 表面，而不考虑覆盖的当前大小。 此属性是可选的。
ms.assetid: fc759013-9dd7-44fc-a0d7-fd2585975966
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE 流媒体设备
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
ms.openlocfilehash: 0804a09708cdd8bd93a5be4e7ba0bc99d2a88838
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188375"
---
# <a name="ksproperty_allocator_control_surface_size"></a>KSPROPERTY \_ 分配器 \_ 控件 \_ 表面 \_ 大小


KSPROPERTY \_ 分配 \_ 器控制 \_ 面 \_ 大小属性通知提供 DirectDraw SURFACE 分配器 (的客户端筛选器，例如覆盖混音) 正在进行捕获操作，并且必须以固定大小分配 Microsoft DirectDraw 表面，而不考虑覆盖的当前大小。 此属性是可选的。

## <span id="ddk_ksproperty_allocator_control_surface_size_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_surface_size_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_surface_size_s)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_SURFACE_SIZE_S</strong></a></p></td>
<td><p>一对 ULONGs</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定覆盖曲面的宽度和高度的一对 ULONGs。

<a name="remarks"></a>备注
-------

支持此属性的微型驱动程序返回一个 KSPROPERTY \_ 分配器 \_ 控制 \_ 图面 \_ 大小 \_ S 结构，该结构描述了所需覆盖面的宽度和高度。 覆盖混音器分配此大小的覆盖面。 如果此值不是 pin 连接期间在媒体大小中指定的大小，则会将视频从视频端口缩放到此大小。 无论 VGA 芯片的缩放能力如何，都不会出现视频端口的其他缩放。

如果混音器通过其主输入插针上的视频端口连接到此属性的上游筛选器，则覆盖混音器始终会查询此新属性。 如果该筛选器未实现此属性，则覆盖混音器会假定它不捕获数据，并根据需要缩放视频端口上的视频以使视频正确显示。

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

[**KSPROPERTY \_ 分配器 \_ 控件 \_ 表面大小为 \_ \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_allocator_control_surface_size_s)

 


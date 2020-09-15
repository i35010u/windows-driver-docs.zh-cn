---
title: KSPROPERTY \_ 首选 \_ 捕获 \_ 图面
description: KSPROPERTY \_ 首选 \_ 捕获 \_ SURFACE 属性返回捕获驱动程序的首选内存目标以便捕获，无论是 VRAM 还是系统内存类型。若要使用 VRAM 传输，捕获微型驱动程序必须支持此属性。
ms.assetid: ed41c456-279d-4728-a85b-f651361ef8e9
keywords:
- KSPROPERTY_PREFERRED_CAPTURE_SURFACE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PREFERRED_CAPTURE_SURFACE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f0006a9c8a1bbd0b48509a75289d70895250eb7
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102388"
---
# <a name="ksproperty_preferred_capture_surface"></a>KSPROPERTY \_ 首选 \_ 捕获 \_ 图面


KSPROPERTY \_ 首选 \_ 捕获 \_ SURFACE 属性返回捕获驱动程序的首选内存目标以便捕获，无论是 VRAM 还是系统内存类型。

若要使用 VRAM 传输，捕获微型驱动程序必须支持此属性。

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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-capture_memory_allocation_flags" data-raw-source="[&lt;strong&gt;CAPTURE_MEMORY_ALLOCATION_FLAGS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-capture_memory_allocation_flags)"><strong>CAPTURE_MEMORY_ALLOCATION_FLAGS</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 首选 \_ 捕获 \_ 图面返回状态 "成功" \_ 以指示已成功完成。 否则，请求将返回相应的错误代码。

<a name="remarks"></a>备注
-------

零是无效的 [**捕获 \_ 内存 \_ 分配 \_ 标志**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-capture_memory_allocation_flags)值。

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


[**捕获 \_ 内存 \_ 分配 \_ 标志**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-capture_memory_allocation_flags)

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)


---
title: KSPROPERTY \_ 映射 \_ \_ \_ 到 \_ VRAM 地址的捕获句柄 \_
description: '\_ \_ VRAM 地址属性的 KSPROPERTY 映射捕获 \_ 句柄 \_ \_ \_ 返回捕获驱动程序将 VRAM surface 控点映射到 VRAM 物理地址。若要使用 VRAM 传输，捕获微型驱动程序必须支持此属性。'
ms.assetid: 071c9152-12f9-4ec1-80d7-6b42fce51bbb
keywords:
- KSPROPERTY_MAP_CAPTURE_HANDLE_TO_VRAM_ADDRESS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_MAP_CAPTURE_HANDLE_TO_VRAM_ADDRESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d0c8b1ae6a03f36a9c0177cb6446173d4fb87b2
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104828"
---
# <a name="ksproperty_map_capture_handle_to_vram_address"></a>KSPROPERTY \_ 映射 \_ \_ \_ 到 \_ VRAM 地址的捕获句柄 \_


\_ \_ VRAM 地址属性的 KSPROPERTY 映射捕获 \_ 句柄 \_ \_ \_ 返回捕获驱动程序将 VRAM surface 控点映射到 VRAM 物理地址。

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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s" data-raw-source="[&lt;strong&gt;VRAM_SURFACE_INFO_PROPERTY_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s)"><strong>VRAM_SURFACE_INFO_PROPERTY_S</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

\_VRAM 地址的 KSPROPERTY 映射 \_ 捕获 \_ 句柄 \_ \_ \_ 返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误代码。

<a name="remarks"></a>备注
-------

捕获驱动程序应在此属性的处理程序中执行映射。

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


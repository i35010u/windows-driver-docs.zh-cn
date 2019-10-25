---
title: KSPROPERTY\_MAP\_捕获\_处理\_到\_VRAM\_ADDRESS
description: KSPROPERTY\_MAP\_捕获\_处理\_到\_VRAM\_ADDRESS 属性返回捕获驱动程序的 VRAM surface 控点到 VRAM 物理地址的映射。若要使用 VRAM 传输，捕获微型驱动程序必须支持此属性。
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
ms.openlocfilehash: a0894363f69405b0d71d2dd470e596386fcf9105
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838050"
---
# <a name="ksproperty_map_capture_handle_to_vram_address"></a>KSPROPERTY\_MAP\_捕获\_处理\_到\_VRAM\_ADDRESS


KSPROPERTY\_MAP\_捕获\_处理\_到\_VRAM\_ADDRESS 属性返回捕获驱动程序的 VRAM surface 控点到 VRAM 物理地址的映射。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s" data-raw-source="[&lt;strong&gt;VRAM_SURFACE_INFO_PROPERTY_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s)"><strong>VRAM_SURFACE_INFO_PROPERTY_S</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_MAP\_捕获\_处理\_到\_VRAM\_ADDRESS 返回状态\_SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误代码。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 







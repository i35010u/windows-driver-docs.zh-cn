---
title: KSPROPERTY\_地图\_捕获\_处理\_TO\_VRAM 能够\_地址
description: KSPROPERTY\_地图\_捕获\_处理\_TO\_vram 能够\_地址属性返回的 vram 能够图面上的句柄捕获驱动程序的映射到 vram 能够物理地址。若要使用 vram 能够传输，捕获微型驱动程序必须支持此属性。
ms.assetid: 071c9152-12f9-4ec1-80d7-6b42fce51bbb
keywords:
- KSPROPERTY_MAP_CAPTURE_HANDLE_TO_VRAM_ADDRESS 流式处理媒体设备
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
ms.openlocfilehash: f352142c99d7e3623de5b401e914f24fcc18651b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524197"
---
# <a name="kspropertymapcapturehandletovramaddress"></a>KSPROPERTY\_地图\_捕获\_处理\_TO\_VRAM 能够\_地址


KSPROPERTY\_地图\_捕获\_处理\_TO\_vram 能够\_地址属性返回的 vram 能够图面上的句柄捕获驱动程序的映射到 vram 能够物理地址。

若要使用 vram 能够传输，捕获微型驱动程序必须支持此属性。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568785" data-raw-source="[&lt;strong&gt;VRAM_SURFACE_INFO_PROPERTY_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568785)"><strong>VRAM_SURFACE_INFO_PROPERTY_S</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_地图\_捕获\_处理\_TO\_vram 能够\_地址返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误代码。

<a name="remarks"></a>备注
-------

此属性的处理程序中，捕获驱动程序应执行映射。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 







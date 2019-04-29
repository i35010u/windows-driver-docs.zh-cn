---
title: KSPROPERTY\_当前\_捕获\_图面
description: KSPROPERTY\_当前\_捕获\_图面上的属性获取或设置使用的给定 pin 捕获内存的类型。若要使用 vram 能够传输，捕获微型驱动程序必须支持此属性。
ms.assetid: fcb07f74-d43a-4850-b8be-c349c92f9f9f
keywords:
- KSPROPERTY_CURRENT_CAPTURE_SURFACE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CURRENT_CAPTURE_SURFACE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8813c23df76d2f92ef2b8027b8f9e0afbfd0ab86
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375191"
---
# <a name="kspropertycurrentcapturesurface"></a>KSPROPERTY\_当前\_捕获\_图面


KSPROPERTY\_当前\_捕获\_图面上的属性获取或设置使用的给定 pin 捕获内存的类型。

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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557647" data-raw-source="[&lt;strong&gt;CAPTURE_MEMORY_ALLOCATION_FLAGS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557647)"><strong>CAPTURE_MEMORY_ALLOCATION_FLAGS</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_当前\_捕获\_面返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误代码。

<a name="remarks"></a>备注
-------

零是无效的值[**捕获\_内存\_分配\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff557647)。

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


[**捕获\_内存\_分配\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff557647)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 







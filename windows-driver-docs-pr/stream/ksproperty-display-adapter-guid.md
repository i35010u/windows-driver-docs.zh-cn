---
title: KSPROPERTY\_DISPLAY\_适配器\_GUID
description: KSPROPERTY\_DISPLAY\_适配器\_GUID 属性从捕获微型驱动程序返回的适配器 GUID。若要使用 vram 能够传输，捕获微型驱动程序必须支持此属性。
ms.assetid: 419aa86e-f1c2-4fca-a9e4-87dcaaeaa2bb
keywords:
- KSPROPERTY_DISPLAY_ADAPTER_GUID 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DISPLAY_ADAPTER_GUID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f18efa02f3cdbcf7bd93b4180ec7276bda6ff3ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543600"
---
# <a name="kspropertydisplayadapterguid"></a>KSPROPERTY\_DISPLAY\_适配器\_GUID


KSPROPERTY\_DISPLAY\_适配器\_GUID 属性从捕获微型驱动程序返回的适配器 GUID。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DISPLAY\_适配器\_GUID 属性将返回状态\_成功以指示已成功完成。 如果属性类型值不正确，它将返回状态\_无效\_参数。

<a name="remarks"></a>备注
-------

微型驱动程序应在 GPU 上返回第一个头适配器的标识符。

捕获 GUID 唯一地标识的捕获设备与之兼容的 vram 能够子系统。 系统提供内核流式处理 (KS) 代理模块 (KsProxy) 使用此 GUID 来分配兼容的 vram 能够子系统上的图面。

AVStream 匹配项的下游 GUID 与此 GUID 呈现 pin 来验证同时捕获和呈现的 pin 是相同的图形适配器上。

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

 

 







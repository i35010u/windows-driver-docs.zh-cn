---
title: KSPROPERTY \_ 显示 \_ 适配器 \_ GUID
description: KSPROPERTY \_ 显示 \_ 适配器 \_ guid 属性从捕获微型驱动程序返回适配器 guid。若要使用 VRAM 传输，捕获微型驱动程序必须支持此属性。
keywords:
- KSPROPERTY_DISPLAY_ADAPTER_GUID 流媒体设备
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
ms.openlocfilehash: 24b4ff3c26424ee31b3f70ef114d2de35ce2fbd5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795817"
---
# <a name="ksproperty_display_adapter_guid"></a>KSPROPERTY \_ 显示 \_ 适配器 \_ GUID


KSPROPERTY \_ 显示 \_ 适配器 \_ guid 属性从捕获微型驱动程序返回适配器 guid。

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
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 显示 \_ 适配器 \_ GUID 属性返回状态 " \_ 成功" 以指示已成功完成。 如果属性类型值不正确，则返回 STATUS \_ 无效 \_ 参数。

<a name="remarks"></a>备注
-------

微型驱动程序应返回 GPU 上第一个头的适配器标识符。

捕获 GUID 唯一地标识了捕获设备兼容的 VRAM 子系统。 系统提供的内核流式处理 (KS) proxy module (KsProxy) 使用此 GUID 在兼容的 VRAM 子系统上分配表面。

AVStream 将此 GUID 与下游呈现器 pin 的 GUID 相匹配，以验证捕获和呈现端口是否在同一图形适配器上。

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


---
title: KSPROPERTY \_ PIN \_ CTYPES
description: 客户端使用 KSPROPERTY \_ 引脚 \_ CTYPES 属性来确定 KS 筛选器支持的 PIN 类型数目。
ms.assetid: 2aa93591-9fe6-453f-bc50-871972cb3e50
keywords:
- KSPROPERTY_PIN_CTYPES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_CTYPES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6307bfad2ecdb9a1e61e2424f3bc1d36b9e85912
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193139"
---
# <a name="ksproperty_pin_ctypes"></a>KSPROPERTY \_ PIN \_ CTYPES


客户端使用 KSPROPERTY \_ 引脚 \_ CTYPES 属性来确定 KS 筛选器支持的 PIN 类型数目。

## <span id="ddk_ksproperty_pin_ctypes_ks"></span><span id="DDK_KSPROPERTY_PIN_CTYPES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

KSPROPERTY \_ 引脚 \_ CTYPES 返回一个类型为 ULONG 的值，指定该 KS 筛选器支持的 PIN 工厂数。

Stream 微型驱动程序不需要直接处理此属性;流类驱动程序使用流请求块处理此属性以查询详细信息。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 


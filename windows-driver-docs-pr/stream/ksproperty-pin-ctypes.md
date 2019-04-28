---
title: KSPROPERTY\_PIN\_CTYPES
description: 客户端使用 KSPROPERTY\_PIN\_CTYPES 属性来确定多少 pin 类型 KS 筛选器支持。
ms.assetid: 2aa93591-9fe6-453f-bc50-871972cb3e50
keywords:
- KSPROPERTY_PIN_CTYPES 流式处理媒体设备
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
ms.openlocfilehash: 0965ac3cbfa779f4a3ddf9238ad7f1d32fc6f0fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346387"
---
# <a name="kspropertypinctypes"></a>KSPROPERTY\_PIN\_CTYPES


客户端使用 KSPROPERTY\_PIN\_CTYPES 属性来确定多少 pin 类型 KS 筛选器支持。

## <span id="ddk_ksproperty_pin_ctypes_ks"></span><span id="DDK_KSPROPERTY_PIN_CTYPES_KS"></span>


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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_PIN\_CTYPES 返回类型为 ULONG，指定的 pin 工厂 KS 筛选器支持的数量的值。

Stream 微型驱动程序不需要直接; 处理此属性stream 类驱动程序处理使用流请求块的详细信息的查询此属性。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 







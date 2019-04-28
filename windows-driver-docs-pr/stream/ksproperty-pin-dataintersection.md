---
title: KSPROPERTY\_PIN\_DATAINTERSECTION
description: 客户端使用 KSPROPERTY\_PIN\_DATAINTERSECTION 属性，若要查找支持 pin 的 pin 工厂实例化的数据格式。 客户端提供一系列数据格式; 数据格式KS 筛选器返回支持列表上的第一个数据格式。
ms.assetid: 447ac37b-1e5e-4812-9e1e-50e9f6f83118
keywords:
- KSPROPERTY_PIN_DATAINTERSECTION 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_DATAINTERSECTION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0a57c7c3eba65539a9296009826b900a81da3b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346383"
---
# <a name="kspropertypindataintersection"></a>KSPROPERTY\_PIN\_DATAINTERSECTION


客户端使用 KSPROPERTY\_PIN\_DATAINTERSECTION 属性，若要查找支持 pin 的 pin 工厂实例化的数据格式。 客户端提供一系列数据格式; 数据格式KS 筛选器返回支持列表上的第一个数据格式。

## <span id="ddk_ksproperty_pin_dataintersection_ks"></span><span id="DDK_KSPROPERTY_PIN_DATAINTERSECTION_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561656" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561656)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

若要指定此属性，提供[ **KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722)结构跟[ **KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)结构和 64 位的序列对齐[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)结构。 **PinId**的成员**KSP\_PIN**指定 pin 工厂。

此属性从客户端提供列表中返回第一个匹配的数据格式。

Stream 微型驱动程序不需要直接; 处理此属性stream 类驱动程序处理使用流请求块的详细信息的查询此属性。

有关详细信息，请参阅[KS 数据格式和数据范围](https://msdn.microsoft.com/library/windows/hardware/ff567632)。

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


[**KSP\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSDATARANGE**](https://msdn.microsoft.com/library/windows/hardware/ff561658)

[**KSDATAFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff561656)

 

 







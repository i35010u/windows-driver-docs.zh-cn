---
title: KSPROPERTY\_PIN\_媒体
description: 此属性返回介质受 pin 由特定 pin 工厂实例化的列表。
ms.assetid: e92c7a3d-4f72-4818-9a26-0e82c20bdb4c
keywords:
- KSPROPERTY_PIN_MEDIUMS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_MEDIUMS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5995b9f6224d259ea95034acbcc29907e20fa24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380817"
---
# <a name="kspropertypinmediums"></a>KSPROPERTY\_PIN\_媒体


此属性返回介质受 pin 由特定 pin 工厂实例化的列表。

## <span id="ddk_ksproperty_pin_mediums_ks"></span><span id="DDK_KSPROPERTY_PIN_MEDIUMS_KS"></span>


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
<td><p>一个<a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"> <strong>KSMULTIPLE_ITEM</strong> </a>结构后, 跟一系列<a href="https://msdn.microsoft.com/library/windows/hardware/ff563538" data-raw-source="[&lt;strong&gt;KSPIN_MEDIUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563538)"> <strong>KSPIN_MEDIUM</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

客户端使用此属性以请求支持的 pin，pin 工厂实例化的所有介质的列表。 客户端然后指定要在连接到的插针时使用的实际介质。

指定此属性使用 KSP\_PIN，其中该成员指定为其返回的媒体列表的 pin 工厂。

KSPROPERTY\_PIN\_媒介返回媒体按照类驱动程序首选项。

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


[**KSP\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSPIN\_MEDIUM**](https://msdn.microsoft.com/library/windows/hardware/ff563538)

 

 







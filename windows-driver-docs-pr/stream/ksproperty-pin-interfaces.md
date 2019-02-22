---
title: KSPROPERTY\_PIN\_接口
description: 此属性返回的受 pin 由特定 pin 工厂实例化的接口的列表。
ms.assetid: 5a49c685-d086-4827-87a3-67d1fa80452a
keywords:
- KSPROPERTY_PIN_INTERFACES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_INTERFACES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 556bc56e96c55b652b84b591e2ca65c89704c8da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544593"
---
# <a name="kspropertypininterfaces"></a>KSPROPERTY\_PIN\_接口


此属性返回的受 pin 由特定 pin 工厂实例化的接口的列表。

## <span id="ddk_ksproperty_pin_interfaces_ks"></span><span id="DDK_KSPROPERTY_PIN_INTERFACES_KS"></span>


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
<td><p>一个<a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"> <strong>KSMULTIPLE_ITEM</strong> </a>结构后, 跟一系列<a href="https://msdn.microsoft.com/library/windows/hardware/ff563537" data-raw-source="[&lt;strong&gt;KSPIN_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563537)"> <strong>KSPIN_INTERFACE</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

指定 KSPROPERTY\_PIN\_接口使用 KSP\_PIN，其中**PinId**成员指定为其返回可用接口的 pin 工厂。

此属性返回按照类驱动程序首选项的接口。

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
<td><p>标头</p></td>
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSMULTIPLE\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSPIN\_INTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff563537)

 

 







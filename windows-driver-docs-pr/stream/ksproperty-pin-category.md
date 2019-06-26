---
title: KSPROPERTY\_PIN\_类别
description: 客户端使用 KSPROPERTY\_PIN\_类别属性来检索 pin 工厂的类别。
ms.assetid: 6579408c-9ec5-4b09-9a63-815cec5bd5a3
keywords:
- KSPROPERTY_PIN_CATEGORY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_CATEGORY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16cc3d0efeae4ba220c547412ad0ebae82c87630
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353216"
---
# <a name="kspropertypincategory"></a>KSPROPERTY\_PIN\_类别


客户端使用 KSPROPERTY\_PIN\_类别属性来检索 pin 工厂的类别。

## <span id="ddk_ksproperty_pin_category_ks"></span><span id="DDK_KSPROPERTY_PIN_CATEGORY_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**PinId**成员的 KSP 的\_PIN 结构指定为其返回类别 GUID 的 pin 工厂。

KS 筛选器使用此属性以指示功能的标准*类别*pin 工厂实例化的 pin。

Stream 微型驱动程序不需要直接; 处理此属性stream 类驱动程序处理使用流请求块来查询有关详细信息，在必要时此属性。

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


[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)

 

 







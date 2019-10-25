---
title: KSPROPERTY\_固定\_类别
description: 客户端使用 KSPROPERTY\_PIN\_CATEGORY 属性来检索 PIN 工厂的类别。
ms.assetid: 6579408c-9ec5-4b09-9a63-815cec5bd5a3
keywords:
- KSPROPERTY_PIN_CATEGORY 流媒体设备
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
ms.openlocfilehash: 6f6dcf6053f24a2abe02d6c264635c312e104ffe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842755"
---
# <a name="ksproperty_pin_category"></a>KSPROPERTY\_固定\_类别


客户端使用 KSPROPERTY\_PIN\_CATEGORY 属性来检索 PIN 工厂的类别。

## <span id="ddk_ksproperty_pin_category_ks"></span><span id="DDK_KSPROPERTY_PIN_CATEGORY_KS"></span>


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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_PIN 结构的**PinId**成员指定要为其返回类别 GUID 的 PIN 工厂。

KS 筛选器使用此属性来指示由 pin 工厂实例化的 pin 的标准功能*类别*。

Stream 微型驱动程序不需要直接处理此属性;流类驱动程序使用流请求块处理此属性，以便在必要时查询详细信息。

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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 







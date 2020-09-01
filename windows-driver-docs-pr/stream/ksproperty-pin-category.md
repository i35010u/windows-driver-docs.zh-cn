---
title: KSPROPERTY \_ PIN \_ 类别
description: 客户端使用 KSPROPERTY \_ pin \_ 类别属性检索 PIN 工厂的类别。
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
ms.openlocfilehash: 40ced99280af3f9a08f74d0cc6ab4d24d2ffc6e7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191051"
---
# <a name="ksproperty_pin_category"></a>KSPROPERTY \_ PIN \_ 类别


客户端使用 KSPROPERTY \_ pin \_ 类别属性检索 PIN 工厂的类别。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP pin 结构的 **PinId** 成员 \_ 指定要为其返回类别 GUID 的 PIN 工厂。

KS 筛选器使用此属性来指示由 pin 工厂实例化的 pin 的标准功能 *类别* 。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 


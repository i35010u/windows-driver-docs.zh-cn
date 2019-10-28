---
title: KSPROPERTY\_PIN\_名称
description: 客户端使用 KSPROPERTY\_PIN\_名称检索 pin 工厂的注册表名称。 这是一个本地化的 Unicode 字符串。
ms.assetid: 763c3116-95f5-4d32-8c46-d8d91f537bd4
keywords:
- KSPROPERTY_PIN_NAME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_NAME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: efe858d254f60c478111f6b59024796d1aa0348b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838852"
---
# <a name="ksproperty_pin_name"></a>KSPROPERTY\_PIN\_名称


客户端使用 KSPROPERTY\_PIN\_名称检索 pin 工厂的注册表名称。 这是一个本地化的 Unicode 字符串。

## <span id="ddk_ksproperty_pin_name_ks"></span><span id="DDK_KSPROPERTY_PIN_NAME_KS"></span>


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
<td><p>一个包含本地化的 Unicode 字符串的缓冲区。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

使用 KSP\_PIN 指定此属性，其中成员指定要为其返回注册表名称的 pin 工厂。

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
<td><p>标头</p></td>
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 

 







---
title: KSPROPERTY \_ PIN \_ 名称
description: 客户端使用 KSPROPERTY 的 \_ pin \_ 名称检索 pin 工厂的注册表名称。 这是一个本地化的 Unicode 字符串。
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
ms.openlocfilehash: 1c62d831518b3f7f45fe5324b227079000c949c3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190893"
---
# <a name="ksproperty_pin_name"></a>KSPROPERTY \_ PIN \_ 名称


客户端使用 KSPROPERTY 的 \_ pin \_ 名称检索 pin 工厂的注册表名称。 这是一个本地化的 Unicode 字符串。

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
<td><p>一个包含本地化的 Unicode 字符串的缓冲区。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

使用 KSP PIN 指定此属性 \_ ，其中成员指定要为其返回注册表名称的 PIN 工厂。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

 


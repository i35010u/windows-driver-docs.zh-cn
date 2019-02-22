---
title: WIA\_IPS\_转移\_扫描
description: WIA\_IPS\_转移\_扫描属性用于启用和配置扫描 （扫描到物理文档边界之外）。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: CAE654BE-B0AC-4182-83CE-C2BDA4792FE4
keywords:
- WIA_IPS_OVER_SCAN 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_OVER_SCAN
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 41b1c1f5235ec72bec364c8afe8776f2b18f22ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525830"
---
# <a name="wiaipsoverscan"></a>WIA\_IPS\_转移\_扫描


**WIA\_IPS\_转移\_扫描**属性用于启用和配置扫描 （扫描到物理文档边界之外）。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_转移\_扫描**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_OVER_SCAN_DISABLED</p></td>
<td><p>通过扫描已禁用。 如果支持该属性，这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_ OVER_SCAN_TOP_BOTTOM</p></td>
<td><p>通过在文档的上边和下边的扫描。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_ OVER_SCAN_LEFT_RIGHT</p></td>
<td><p>通过在左侧和右侧的文档扫描。</p></td>
</tr>
<tr class="even">
<td><p>所有 WIA_ OVER_SCAN_</p></td>
<td><p>通过在文档的所有边的扫描。</p></td>
</tr>
</tbody>
</table>

 

此属性仅适用于所有可编程图像数据源项，包括平板 (WIA\_类别\_平板) 和送纸器 (WIA\_类别\_送纸器) 和是可选的。 支持的属性，当 WIA\_转移\_扫描\_禁用是所需的默认值。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 






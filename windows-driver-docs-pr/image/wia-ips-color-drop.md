---
title: WIA\_IPS\_颜色\_删除
description: WIA\_IPS\_颜色\_下拉属性用于配置筛选从硬件设备获取的图像数据的颜色。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: A0F14FDF-194D-4948-B9D8-F3E0C2E34618
keywords:
- WIA_IPS_COLOR_DROP 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_COLOR_DROP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4186e43792528d14a3629ae1c76cb5cfb1f09379
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533078"
---
# <a name="wiaipscolordrop"></a>WIA\_IPS\_颜色\_删除


**WIA\_IPS\_颜色\_删除**属性用于配置筛选从硬件设备获取的图像数据的颜色。 WIA 微型驱动程序创建并维护此属性。



属性类型：VT\_I4 

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_颜色\_删除**属性。

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
<td><p>WIA_COLOR_DROP_DISABLED</p></td>
<td><p>颜色放置处于禁用状态。 如果支持该属性，这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_COLOR_DROP_RED</p></td>
<td><p>红色通道放入所描述的金额<a href="wia-ips-color-drop-red.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_RED&lt;/strong&gt;](wia-ips-color-drop-red.md)"> <strong>WIA_IPS_COLOR_DROP_RED</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COLOR_DROP_GREEN</p></td>
<td><p>绿色通道放入所描述的金额<a href="wia-ips-color-drop-green.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_GREEN&lt;/strong&gt;](wia-ips-color-drop-green.md)"> <strong>WIA_IPS_COLOR_DROP_GREEN</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p>WIA_COLOR_DROP_BLUE</p></td>
<td><p>蓝色通道放入所描述的金额<a href="wia-ips-color-drop-blue.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_BLUE&lt;/strong&gt;](wia-ips-color-drop-blue.md)"> <strong>WIA_IPS_COLOR_DROP_BLUE</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COLOR_DROP_RGB</p></td>
<td><p>在指定的金额中将被删除的红色、 绿色和/或蓝色通道<a href="wia-ips-color-drop-red.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_RED&lt;/strong&gt;](wia-ips-color-drop-red.md)"> <strong>WIA_IPS_COLOR_DROP_RED</strong></a>， <a href="wia-ips-color-drop-green.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_GREEN&lt;/strong&gt;](wia-ips-color-drop-green.md)"> <strong>WIA_IPS_COLOR_DROP_GREEN</strong> </a>，并<a href="wia-ips-color-drop-blue.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_BLUE&lt;/strong&gt;](wia-ips-color-drop-blue.md)"> <strong>WIA_IPS_COLOR_DROP_BLUE</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

此属性仅适用于所有可编程图像数据源项，包括平板 (WIA\_类别\_平板) 和送纸器 (WIA\_类别\_送纸器) 和是可选的。 支持的属性，当 WIA\_颜色\_DROP\_禁用是所需的默认值。

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

 

 






---
title: WIA \_ IP \_ 颜色 \_ 放置
description: WIA \_ ip \_ 颜色 \_ DROP 属性用于配置从硬件设备获取的图像数据的颜色筛选。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_COLOR_DROP 图像设备
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
ms.openlocfilehash: d054366f58a08357d286c9754771d8702c8d2f1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828685"
---
# <a name="wia_ips_color_drop"></a>WIA \_ IP \_ 颜色 \_ 放置


**WIA \_ ip \_ 颜色 \_ DROP** 属性用于配置从硬件设备获取的图像数据的颜色筛选。 WIA 微型驱动程序创建并维护此属性。



属性类型： VT \_ I4 

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 **WIA \_ ip \_ 颜色 \_ DROP** 属性的有效值。

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
<td><p>禁用颜色删除。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_COLOR_DROP_RED</p></td>
<td><p>红色通道按 <a href="wia-ips-color-drop-red.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_RED&lt;/strong&gt;](wia-ips-color-drop-red.md)"><strong>WIA_IPS_COLOR_DROP_RED</strong></a>所述的数量被丢弃。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COLOR_DROP_GREEN</p></td>
<td><p>绿色频道会按 <a href="wia-ips-color-drop-green.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_GREEN&lt;/strong&gt;](wia-ips-color-drop-green.md)"><strong>WIA_IPS_COLOR_DROP_GREEN</strong></a>所述的数量进行下降。</p></td>
</tr>
<tr class="even">
<td><p>WIA_COLOR_DROP_BLUE</p></td>
<td><p>蓝色通道按 <a href="wia-ips-color-drop-blue.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_BLUE&lt;/strong&gt;](wia-ips-color-drop-blue.md)"><strong>WIA_IPS_COLOR_DROP_BLUE</strong></a>所述的数量被丢弃。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COLOR_DROP_RGB</p></td>
<td><p>红色、绿色和/或蓝色通道按照 <a href="wia-ips-color-drop-red.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_RED&lt;/strong&gt;](wia-ips-color-drop-red.md)"><strong>WIA_IPS_COLOR_DROP_RED</strong></a>、 <a href="wia-ips-color-drop-green.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_GREEN&lt;/strong&gt;](wia-ips-color-drop-green.md)"><strong>WIA_IPS_COLOR_DROP_GREEN</strong></a>和 <a href="wia-ips-color-drop-blue.md" data-raw-source="[&lt;strong&gt;WIA_IPS_COLOR_DROP_BLUE&lt;/strong&gt;](wia-ips-color-drop-blue.md)"><strong>WIA_IPS_COLOR_DROP_BLUE</strong></a>指定的数量删除。</p></td>
</tr>
</tbody>
</table>

 

此属性对所有可编程的图像数据源项有效，包括平板 (WIA \_ 类别 \_ 平板) 和送纸器 (wia \_ 类别 \_ 进纸器) ，并且是可选的。 如果支持该属性，则 \_ 禁用 WIA 颜色 \_ 删除 \_ 是所需的默认值。

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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 






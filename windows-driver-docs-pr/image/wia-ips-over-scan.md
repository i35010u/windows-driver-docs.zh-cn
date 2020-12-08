---
title: WIA \_ IP \_ 超过 \_ 扫描
description: WIA \_ IPS \_ OVER \_ SCAN 属性用于启用和配置扫描 (扫描超出物理文档边界) 。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_OVER_SCAN 图像设备
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
ms.openlocfilehash: 4f7113ceccebc1eaa0e8f2dff08e51ca4843327d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823141"
---
# <a name="wia_ips_over_scan"></a>WIA \_ IP \_ 超过 \_ 扫描


**WIA \_ IPS \_ OVER \_ SCAN** 属性用于启用和配置扫描 (扫描超出物理文档边界) 。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 **WIA \_ ip \_ OVER \_ SCAN** 属性的有效值。

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
<td><p>禁用扫描。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_ OVER_SCAN_TOP_BOTTOM</p></td>
<td><p>在文档的顶部和底部进行扫描。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_ OVER_SCAN_LEFT_RIGHT</p></td>
<td><p>在文档的左侧和右侧多次扫描。</p></td>
</tr>
<tr class="even">
<td><p>全部 OVER_SCAN_ WIA_</p></td>
<td><p>在文档的所有各面上进行扫描。</p></td>
</tr>
</tbody>
</table>

 

此属性对所有可编程的图像数据源项有效，包括平板 (WIA \_ 类别 \_ 平板) 和送纸器 (wia \_ 类别 \_ 进纸器) ，并且是可选的。 如果支持该属性，则 \_ \_ \_ "禁用扫描时禁用 WIA" 是所需的默认值。

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

 

 






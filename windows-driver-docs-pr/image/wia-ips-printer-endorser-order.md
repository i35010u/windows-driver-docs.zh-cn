---
title: WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 订单
description: WIA \_ IPS \_ PRINTER \_ ENDORSER \_ ORDER 属性用于配置要相对于彼此执行扫描和 imprinting/认可操作的顺序。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_PRINTER_ENDORSER_ORDER 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_ORDER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 587088c74182949ca536d5281668dd6e740fb3a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839527"
---
# <a name="wia_ips_printer_endorser_order"></a>WIA \_ IPS \_ 打印机 \_ ENDORSER \_ 订单


**WIA \_ IPS \_ PRINTER \_ ENDORSER \_ ORDER** 属性用于配置要相对于彼此执行扫描和 imprinting/认可操作的顺序。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

下表介绍了在 " [**WIA \_ ip \_ 预览 \_ 类型**](wia-ips-preview-type.md) " 属性中有效的常量。

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
<td><p>WIA_PRINTER_ENDORSER_BEFORE_SCAN</p></td>
<td><p>在扫描此文档页面之前，将在文档页面上执行打印/认可。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_AFTER_SCAN</p></td>
<td><p>扫描此文档页后，将在文档页上执行打印/认可。</p></td>
</tr>
</tbody>
</table>

 

此属性必须受所有 Imprinter/Endorser 数据源项支持。 无必需的默认值。

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

 

 






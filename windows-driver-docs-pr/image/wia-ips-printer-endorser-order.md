---
title: WIA\_IPS\_打印机\_印记签署器\_顺序
description: WIA\_IPS\_打印机\_印记签署器\_顺序属性用于配置在其中的扫描和认可 imprinting/操作都要执行相对于彼此的顺序。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: DE146E16-C956-497D-BAF5-F7CE6FAF382B
keywords:
- WIA_IPS_PRINTER_ENDORSER_ORDER 成像设备
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
ms.openlocfilehash: e6f322a6a021c5c4a965ea7a32ba34c1750b88fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520617"
---
# <a name="wiaipsprinterendorserorder"></a>WIA\_IPS\_打印机\_印记签署器\_顺序


**WIA\_IPS\_打印机\_印记签署器\_顺序**属性用于配置在其中的扫描和认可 imprinting/操作是相对于每个要执行的顺序其他。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了与有效的常量[ **WIA\_IPS\_预览\_类型**](wia-ips-preview-type.md)属性。

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
<td><p>扫描此文档页之前，认可打印/是文档页面上执行。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_AFTER_SCAN</p></td>
<td><p>在此文档页扫描之后，认可打印/是文档页面上执行。</p></td>
</tr>
</tbody>
</table>

 

此属性必须受所有印刷器/印记签署器数据源项。 没有所需的默认值。

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

 

 






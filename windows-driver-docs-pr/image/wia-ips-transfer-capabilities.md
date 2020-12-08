---
title: WIA \_ IPS \_ 传输 \_ 功能
description: "\"WIA \\_ IPS \\_ 传输 \\_ 功能\" 属性用于指示设备是否可以同时传输父项和子项。 WIA 微型驱动程序创建并维护此属性。"
keywords:
- WIA_IPS_TRANSFER_CAPABILITIES 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_TRANSFER_CAPABILITIES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53b2f7103f91bc929774794b82a9aa865d55f5ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814407"
---
# <a name="wia_ips_transfer_capabilities"></a>WIA \_ IPS \_ 传输 \_ 功能


"WIA \_ IPS \_ 传输 \_ 功能" 属性用于指示设备是否可以同时传输父项和子项。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了对 "WIA \_ IPS \_ 传输 \_ 功能" 属性有效的常量

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>标志</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_TRANSFER_CHILDREN_SINGLE_SCAN</p></td>
<td><p>设备可以将父项和子项一起传输，或者设备必须为每个项目和每个子项目单独进行扫描。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 






---
title: WIA \_ IP \_ 灯
description: WIA \_ IPS \_ 灯泡属性包含扫描仪灯泡的当前配置设置。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_LAMP 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_LAMP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf64b85a5eb24d6db303fe2d8b12aa58eaf9f200
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825973"
---
# <a name="wia_ips_lamp"></a>WIA \_ IP \_ 灯


WIA \_ IPS \_ 灯泡属性包含扫描仪灯泡的当前配置设置。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

使用 "WIA \_ IPS \_ 灯泡" 属性，可以以编程方式控制扫描仪灯; 此灯可能是透明适配器的专用灯具 () 或专用胶片扫描器) 的主扫描仪灯泡 (。

下表描述了对 WIA ip 灯具有效的常量 \_ \_ 。

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
<td><p>WIA_LAMP_ON</p></td>
<td><p>灯为 on。</p></td>
</tr>
<tr class="even">
<td><p>WIA_LAMP_OFF</p></td>
<td><p>灯泡处于关闭状态。</p></td>
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

 

 






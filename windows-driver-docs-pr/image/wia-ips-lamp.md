---
title: WIA\_IPS\_LAMP
description: WIA\_IP\_LAMP 属性包含扫描仪的 lamp 的当前配置设置。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: a5eb83cf-824a-4c7c-a7e3-2f9af5a2eb3c
keywords:
- WIA_IPS_LAMP 成像设备
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
ms.openlocfilehash: 8f14e2d229cf684ff0828dd227da7609fda5c679
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348234"
---
# <a name="wiaipslamp"></a>WIA\_IPS\_LAMP


WIA\_IP\_LAMP 属性包含扫描仪的 lamp 的当前配置设置。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_IP\_LAMP 属性，以编程方式控制的扫描程序 lamp; 此 lamp 可能是专用的 lamp （适用于的透明度适配器） 或 （适用于专用的电影扫描程序） 的主要扫描程序灯泡。

下表描述了有效使用 WIA 的常量\_IP\_LAMP。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_LAMP_ON</p></td>
<td><p>灯泡是上。</p></td>
</tr>
<tr class="even">
<td><p>WIA_LAMP_OFF</p></td>
<td><p>Lamp 处于关闭状态。</p></td>
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
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 






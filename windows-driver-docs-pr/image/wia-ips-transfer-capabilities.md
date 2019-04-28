---
title: WIA\_IPS\_传输\_功能
description: WIA\_IPS\_传输\_功能属性指示是否设备可以一起传输父项和子项。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 937e3e54-6ad3-46bb-bd00-e0812c64e539
keywords:
- WIA_IPS_TRANSFER_CAPABILITIES 成像设备
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
ms.openlocfilehash: 74beb9d4cb749e5cf8fb9345fbbb4a03515701c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343825"
---
# <a name="wiaipstransfercapabilities"></a>WIA\_IPS\_传输\_功能


WIA\_IPS\_传输\_功能属性指示是否设备可以一起传输父项和子项。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了常量，它是有效使用 WIA\_IPS\_传输\_功能属性

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_TRANSFER_CHILDREN_SINGLE_SCAN</p></td>
<td><p>设备可以一起传输的父级和子级的项或设备必须进行单独扫描每个项和每个子项。</p></td>
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

 

 






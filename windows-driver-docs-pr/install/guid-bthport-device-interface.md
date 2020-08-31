---
title: GUID_BTHPORT_DEVICE_INTERFACE
description: GUID_BTHPORT_DEVICE_INTERFACE
ms.assetid: 2e23912c-ab5b-4c4d-94c7-e763544cc2f5
keywords:
- GUID_BTHPORT_DEVICE_INTERFACE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_BTHPORT_DEVICE_INTERFACE
api_location:
- Bthdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9f288f533d662c5a114c0a62177513214aa8f249
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095711"
---
# <a name="guid_bthport_device_interface"></a>GUID_BTHPORT_DEVICE_INTERFACE


为[蓝牙无线电收发](/previous-versions/windows/hardware/drivers/ff536596(v=vs.85))器定义了 GUID_BTHPORT_DEVICE_INTERFACE[设备接口类](./overview-of-device-interface-classes.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_BTHPORT_DEVICE_INTERFACE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{0850302A-B344-4fda-9BE9-90576B8D46F0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

[蓝牙无线电](/previous-versions/windows/hardware/drivers/ff536596(v=vs.85))设备的驱动程序注册此设备接口类的实例，通知操作系统和应用程序是否存在蓝牙无线电收发器。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows Vista、Windows XP SP2 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Bthdef (包含 Bthdef) </td>
</tr>
</tbody>
</table>

 


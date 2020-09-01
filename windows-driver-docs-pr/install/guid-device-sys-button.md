---
title: GUID_DEVICE_SYS_BUTTON
description: GUID_DEVICE_SYS_BUTTON
ms.assetid: 6d07e015-3ea5-4951-ab2d-9c110edef1c5
keywords:
- GUID_DEVICE_SYS_BUTTON 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVICE_SYS_BUTTON
api_location:
- Poclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 476304c3b4ffd1f7efdb32ec01f99f5b193c34d7
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096977"
---
# <a name="guid_device_sys_button"></a>GUID_DEVICE_SYS_BUTTON


GUID_DEVICE_SYS_BUTTON [设备接口类](./overview-of-device-interface-classes.md)定义为高级配置和电源接口 (ACPI) 系统电源按钮设备。

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
<td align="left"><p>GUID_DEVICE_SYS_BUTTON</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{4AFA3D53-74A7-11d0-be5e-00A0C9062857}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的 [ACPI 驱动程序](../kernel/acpi-driver.md) 将注册此设备接口类的实例，通知操作系统和应用程序是否存在系统电源按钮设备。 I8042prt 是系统提供的 PS/2 样式键盘和鼠标设备驱动程序，还为支持系统电源按钮的键盘注册此类的实例。

有关为 ACPI 设备提供 WDM [函数驱动程序](../kernel/function-drivers.md) 的信息，请参阅 [支持 acpi 设备](../acpi/supporting-acpi-devices.md)。

有关 PS/2 样式键盘和鼠标设备的信息，请参阅 [非 HIDClass 键盘和鼠标设备](../hid/keyboard-and-mouse-class-drivers.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Poclass (包含 Poclass) </td>
</tr>
</tbody>
</table>

 


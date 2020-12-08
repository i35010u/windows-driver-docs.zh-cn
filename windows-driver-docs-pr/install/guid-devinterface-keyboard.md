---
title: GUID_DEVINTERFACE_KEYBOARD
description: GUID_DEVINTERFACE_KEYBOARD
keywords:
- GUID_DEVINTERFACE_KEYBOARD 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_KEYBOARD
api_location:
- Ntddkbd.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dc09cb4a804d574bbe0ed4bdebe0731cab5bccdd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798125"
---
# <a name="guid_devinterface_keyboard"></a>GUID_DEVINTERFACE_KEYBOARD


为键盘设备定义 GUID_DEVINTERFACE_KEYBOARD [设备接口类](./overview-of-device-interface-classes.md) 。

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
<td align="left"><p>GUID_DEVINTERFACE_KEYBOARD</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{884b96c3-56ef-11d1-bc8c-00a0c91405dd}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

键盘设备的驱动程序注册此设备接口类的实例，以通知系统和应用程序是否存在键盘设备。

系统提供的 [键盘类驱动程序](../hid/keyboard-and-mouse-class-drivers.md) 为键盘设备注册此设备接口类的实例。 使用键盘类驱动程序所支持的 i/o 接口访问此设备接口类的实例。

有关支持键盘设备的常规信息，请参阅[Kbdclass 和 Mouclass 驱动程序](../hid/keyboard-and-mouse-class-drivers.md)的[HID 体系结构](../hid/hid-architecture.md)和功能。

WDK 包含系统提供的键盘类驱动程序的示例代码。 键盘类驱动程序使用过时的标识符 [**GUID_CLASS_KEYBOARD**](guid-class-keyboard.md) 来注册此 [设备安装程序类](./overview-of-device-setup-classes.md)的实例。

有关用于鼠标设备的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)。

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
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddkbd (包含 Ntddkbd) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_CLASS_KEYBOARD**](guid-class-keyboard.md)

[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 


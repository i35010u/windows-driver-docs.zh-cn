---
title: GUID_DEVINTERFACE_MOUSE
description: GUID_DEVINTERFACE_MOUSE
ms.assetid: c5aff960-a78d-4429-ba3f-f2f91d9a56fa
keywords:
- GUID_DEVINTERFACE_MOUSE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_MOUSE
api_location:
- Ntddmou.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6e6511b0d4533d07cd66eca9f0820900d0462dd9
ms.sourcegitcommit: 735fea11056fe943c4368ee54573790e0602de66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91979986"
---
# <a name="guid_devinterface_mouse"></a>GUID_DEVINTERFACE_MOUSE


为鼠标设备定义 GUID_DEVINTERFACE_MOUSE [设备接口类](./overview-of-device-interface-classes.md) 。

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
<td align="left"><p>GUID_DEVINTERFACE_MOUSE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{378DE44C-56EF-11D1-BC8C-00A0C91405DD}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

鼠标设备的驱动程序注册此设备接口类的实例，通知操作系统和应用程序是否存在鼠标设备。

系统提供的 [鼠标类驱动程序](../hid/keyboard-and-mouse-class-drivers.md) 为鼠标设备注册此设备接口类的实例。 使用鼠标类驱动程序所支持的 i/o 接口访问此设备接口类的实例。

有关支持鼠标设备的常规信息，请参阅[Kbdclass 和 Mouclass 驱动程序](../hid/keyboard-and-mouse-class-drivers.md)的[HID 体系结构](../hid/hid-architecture.md)和功能。

WDK 包含系统提供的鼠标类驱动程序的示例代码。 鼠标类驱动程序使用过时的标识符 [**GUID_CLASS_MOUSE**](guid-class-mouse.md) 来注册此 [设备安装程序类](./overview-of-device-setup-classes.md)的实例。

有关键盘设备的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)。

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
<td align="left"><p>标题</p></td>
<td align="left">Ntddmou (包含 Ntddmou) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_CLASS_MOUSE**](guid-class-mouse.md)

[**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)

 


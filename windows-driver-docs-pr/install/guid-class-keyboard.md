---
title: GUID_CLASS_KEYBOARD
description: GUID_CLASS_KEYBOARD
keywords:
- GUID_CLASS_KEYBOARD 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_CLASS_KEYBOARD
api_location:
- Ntddkbd.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0d60e75ab1321797af52fd365049ba468a3486a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796109"
---
# <a name="guid_class_keyboard"></a>GUID_CLASS_KEYBOARD


GUID_CLASS_KEYBOARD 是键盘设备的 [设备接口类](./overview-of-device-interface-classes.md) 的过时标识符。 从 Microsoft Windows 2000 开始，使用此类的新实例 [**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md) 类标识符。

<a name="remarks"></a>备注
-------

WDK 中提供的 HID 示例包括键盘类驱动程序。 键盘类驱动程序使用 GUID_CLASS_KEYBOARD 来注册此设备接口类的实例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_KEYBOARD。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddkbd (包含 Ntddkbd) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)

 


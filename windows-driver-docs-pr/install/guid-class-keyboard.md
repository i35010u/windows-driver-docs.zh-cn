---
title: GUID_CLASS_KEYBOARD
description: GUID_CLASS_KEYBOARD
ms.assetid: 9e90d18f-5298-4234-8b05-38e9b8ec5076
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
ms.openlocfilehash: aa4609a633d8f89cabe6108d21201bcca0877a95
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094935"
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

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)

 


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
ms.openlocfilehash: 5fa3bb8af6d7171074c8a235a4d59621cfcb7789
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533941"
---
# <a name="guiddevinterfacemouse"></a>GUID_DEVINTERFACE_MOUSE


GUID_DEVINTERFACE_MOUSE[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)定义适用于鼠标设备。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
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

 

<a name="remarks"></a>备注
-------

鼠标设备的驱动程序注册通知的操作系统和应用程序的鼠标设备存在此设备接口类的实例。

系统提供[鼠标类驱动程序](../hid/keyboard-and-mouse-class-drivers.md)注册此鼠标设备的设备接口类的实例。 通过使用鼠标类驱动程序支持的 I/O 接口中访问此设备接口类的实例。

有关支持鼠标设备的常规信息，请参阅[HID 体系结构](https://msdn.microsoft.com/library/windows/hardware/jj126193)并[Kbdclass 和 Mouclass 驱动程序的功能](../hid/keyboard-and-mouse-class-drivers.md)。

WDK 包含系统提供鼠标类驱动程序的示例代码。 鼠标类驱动程序将使用已过时的标识符[ **GUID_CLASS_MOUSE** ](guid-class-mouse.md)若要注册此实例[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。

有关键盘的设备的设备接口类的信息，请参阅[ **GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)。

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
<td align="left">Ntddmou.h （包括 Ntddmou.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_CLASS_MOUSE**](guid-class-mouse.md)

[**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)

 

 







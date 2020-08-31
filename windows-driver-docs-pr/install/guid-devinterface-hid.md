---
title: GUID_DEVINTERFACE_HID
description: GUID_DEVINTERFACE_HID
ms.assetid: af2ebdaf-b7e9-4f79-abb6-60f1fb954b55
keywords:
- GUID_DEVINTERFACE_HID 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_HID
api_location:
- Hidclass.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fc9783a14d5e9bf1e7cf6e0b7fe67d58fa4b9e96
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095223"
---
# <a name="guid_devinterface_hid"></a>GUID_DEVINTERFACE_HID


GUID_DEVINTERFACE_HID [设备接口类](./overview-of-device-interface-classes.md) 是为 [HID 集合](../hid/hid-collections.md)定义的。

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
<td align="left"><p>GUID_DEVINTERFACE_HID</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{4D1E55B2-F16F-11CF-88CB-001111000030}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

HID 集合的驱动程序注册此设备接口类的实例，通知操作系统和应用程序是否存在 HID 集合。

系统提供的 [hid 类驱动程序](/previous-versions/jj126193(v=vs.85)) 为 HID 集合注册此设备接口类的实例。 例如，HID 类驱动程序为 USB 键盘或鼠标设备注册接口。 使用 HID 类驱动程序支持的 i/o 接口访问 HID 集合。

有关 HID 设备和驱动程序的信息，请参阅 [HIDClass 设备](../hid/binding-minidrivers-to-the-hid-class.md)。

有关键盘设备的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)。

有关用于鼠标设备的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)。

[**GUID_CLASS_INPUT**](guid-class-input.md)是此设备接口类的过时标识符;改用 GUID_DEVINTERFACE_HID。

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
<td align="left">Hidclass (包含 Hidclass) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_CLASS_INPUT**](guid-class-input.md)

[**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)

[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 


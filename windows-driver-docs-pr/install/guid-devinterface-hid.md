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
ms.openlocfilehash: 78668560a88fb8e926544e28471b559f485cb120
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391543"
---
# <a name="guiddevinterfacehid"></a>GUID_DEVINTERFACE_HID


GUID_DEVINTERFACE_HID[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[HID 集合](https://docs.microsoft.com/windows-hardware/drivers/hid/hid-collections)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
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

HID 集合的驱动程序注册通知的操作系统和应用程序的 HID 集合存在此设备接口类的实例。

系统提供[HID 类驱动程序](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))注册 HID 集合将此设备接口类的实例。 例如，HID 类驱动程序注册为 USB 键盘或鼠标设备的接口。 通过使用支持的 HID 类驱动程序的 I/O 接口访问 HID 集合。

有关 HID 设备和驱动程序的信息，请参阅[HIDClass 设备](../hid/binding-minidrivers-to-the-hid-class.md)。

有关键盘的设备的设备接口类的信息，请参阅[ **GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)。

鼠标设备的设备接口类有关的信息，请参阅[ **GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)。

[ **GUID_CLASS_INPUT** ](guid-class-input.md)是此设备的已过时标识符接口类; 请改用 GUID_DEVINTERFACE_HID。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Hidclass.h （包括 Hidclass.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_CLASS_INPUT**](guid-class-input.md)

[**GUID_DEVINTERFACE_KEYBOARD**](guid-devinterface-keyboard.md)

[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 

 







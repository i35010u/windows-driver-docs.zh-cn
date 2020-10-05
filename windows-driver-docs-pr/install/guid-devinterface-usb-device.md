---
title: GUID_DEVINTERFACE_USB_DEVICE
description: GUID_DEVINTERFACE_USB_DEVICE
ms.assetid: 9a771eca-8ec5-4c69-8b1e-f01f548b5041
keywords:
- GUID_DEVINTERFACE_USB_DEVICE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_USB_DEVICE
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b0aeb5f54f2d92e0c3c365eea55f6ae651ba6f30
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732853"
---
# <a name="guid_devinterface_usb_device"></a>GUID_DEVINTERFACE_USB_DEVICE


为连接到 USB 集线器的[usb 设备](../index.yml)定义 GUID_DEVINTERFACE_USB_DEVICE[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>GUID_DEVINTERFACE_USB_DEVICE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{A5DCBF10-6530-11D2-901F-00C04FB951ED}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的 USB 集线器驱动程序将注册 GUID_DEVINTERFACE_USB_DEVICE 的实例，以通知系统和应用程序是否存在连接到 USB 集线器的 USB 设备。

Microsoft Windows 驱动程序工具包 (WDK) 包含 [USBVIEW 示例应用程序](/samples/browse/)。 USBVIEW 示例使用过时的标识符 [**GUID_CLASS_USB_DEVICE**](guid-class-usb-device.md) 来注册，以获得此设备接口类的实例到达时的通知。

必须包含 initguid.h，然后才能包含使用 DEFINE_GUID 宏声明 GUID 的任何标头。

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
<td align="left">Usbiodef (包含 Usbiodef，initguid.h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_CLASS_USB_DEVICE**](guid-class-usb-device.md)

[**GUID_DEVINTERFACE_USB_HOST_CONTROLLER**](guid-devinterface-usb-host-controller.md)

[**GUID_DEVINTERFACE_USB_HUB**](guid-devinterface-usb-hub.md)


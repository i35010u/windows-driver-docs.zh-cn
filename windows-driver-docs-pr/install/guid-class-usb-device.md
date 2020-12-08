---
title: GUID_CLASS_USB_DEVICE
description: GUID_CLASS_USB_DEVICE
keywords:
- GUID_CLASS_USB_DEVICE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_CLASS_USB_DEVICE
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fdb52f322dc9ef593cfe1bce17c8699cb9216a00
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796095"
---
# <a name="guid_class_usb_device"></a>GUID_CLASS_USB_DEVICE


GUID_CLASS_USB_DEVICE 是连接到 USB 集线器的[usb](../index.yml)设备的[设备接口类](./overview-of-device-interface-classes.md)的过时标识符。 从 Microsoft Windows 2000 开始，使用此类的新实例 [**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md) 类标识符。

## <a name="remarks"></a>备注

Microsoft Windows 驱动程序工具包 (WDK) 包含 [USBVIEW 示例应用程序](/samples/browse/)。 USBVIEW 示例使用 GUID_CLASS_USB_DEVICE 进行注册，以便在存在 GUID_CLASS_USB_DEVICE 接口类的实例时收到通知。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_USB_DEVICE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Usbiodef (包含 Usbiodef) </td>
</tr>
</tbody>
</table>

以前，此标识符依赖于 `Usbioctl.h` 。  请注意，现在需要包含 `Usbiodef.h` 。

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)


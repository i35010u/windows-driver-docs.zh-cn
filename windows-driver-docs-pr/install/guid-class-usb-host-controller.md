---
title: GUID_CLASS_USB_HOST_CONTROLLER
description: GUID_CLASS_USB_HOST_CONTROLLER
ms.assetid: d2140a9e-95bc-48dd-a80b-3b098937edb3
keywords:
- GUID_CLASS_USB_HOST_CONTROLLER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_CLASS_USB_HOST_CONTROLLER
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d32c6cfb010daaf79efe8f7485fe633a0cc8da9c
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733519"
---
# <a name="guid_class_usb_host_controller"></a>GUID_CLASS_USB_HOST_CONTROLLER


GUID_CLASS_USB_HOST_CONTROLLER 是[USB](../index.yml)主机控制器设备的[设备接口类](./overview-of-device-interface-classes.md)的过时标识符。 从 Microsoft Windows 2000 开始，使用此类的新实例 [**GUID_DEVINTERFACE_USB_HOST_CONTROLLER**](guid-devinterface-usb-host-controller.md) 类标识符。

<a name="remarks"></a>备注
-------

Microsoft Windows 驱动程序工具包 (WDK) 包含 [USBVIEW 示例应用程序](/samples/browse/)。 USBVIEW 示例使用 GUID_CLASS_USB_HOST_CONTROLLER 枚举 GUID_CLASS_USB_HOST_CONTROLLER 设备接口类的实例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_USB_HOST_CONTROLLER。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Usbiodef (包含 Usbiodef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_USB_HOST_CONTROLLER**](guid-devinterface-usb-host-controller.md)


---
title: GUID_DEVINTERFACE_USB_HOST_CONTROLLER
description: GUID_DEVINTERFACE_USB_HOST_CONTROLLER
keywords:
- GUID_DEVINTERFACE_USB_HOST_CONTROLLER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_USB_HOST_CONTROLLER
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: efac81b76687877621f91b77ba32d5ce6e9288f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819503"
---
# <a name="guid_devinterface_usb_host_controller"></a>GUID_DEVINTERFACE_USB_HOST_CONTROLLER


为[USB](../index.yml)主机控制器设备定义 GUID_DEVINTERFACE_USB_HOST_CONTROLLER[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>GUID_DEVINTERFACE_USB_HOST_CONTROLLER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{3ABF6F2D-71C4-462A-8A92-1E6861E6AF27}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的 USB 主机控制器端口驱动程序将注册 GUID_DEVINTERFACE_USB_HOST_CONTROLLER 的实例，以通知操作系统和存在 USB 主机控制器的应用程序。

Microsoft Windows 驱动程序工具包 (WDK) 包含 [USBVIEW 示例应用程序](/samples/browse/)。 USBVIEW 使用已过时的标识符 [**GUID_CLASS_USB_HOST_CONTROLLER**](guid-class-usb-host-controller.md) 来枚举此设备接口类的实例。

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

## <a name="see-also"></a>请参阅


[**GUID_CLASS_USB_HOST_CONTROLLER**](guid-class-usb-host-controller.md)

[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

[**GUID_DEVINTERFACE_USB_HUB**](guid-devinterface-usb-hub.md)


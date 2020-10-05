---
title: GUID_DEVINTERFACE_USB_HOST_CONTROLLER
description: GUID_DEVINTERFACE_USB_HOST_CONTROLLER
ms.assetid: 4afa1ada-ff57-4585-9117-10595310b976
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
ms.openlocfilehash: deb561684d55230630741a1ea48a0070466afd9b
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732855"
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
<th align="left">属性</th>
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

## <a name="see-also"></a>另请参阅


[**GUID_CLASS_USB_HOST_CONTROLLER**](guid-class-usb-host-controller.md)

[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

[**GUID_DEVINTERFACE_USB_HUB**](guid-devinterface-usb-hub.md)


---
title: GUID_DEVINTERFACE_USB_HUB
description: GUID_DEVINTERFACE_USB_HUB
keywords:
- GUID_DEVINTERFACE_USB_HUB 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_USB_HUB
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 96c9a844edce948036d44429b35f25adc3f39ed7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839081"
---
# <a name="guid_devinterface_usb_hub"></a>GUID_DEVINTERFACE_USB_HUB


为[USB](../index.yml)集线器设备定义 GUID_DEVINTERFACE_USB_HUB[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>GUID_DEVINTERFACE_USB_HUB</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{F18A0E88-C30C-11D0-8815-00A0C906BED8}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的 USB 端口驱动程序将注册 GUID_DEVINTERFACE_USB_HUB 的实例，以通知操作系统和应用程序是否存在主机控制器设备的根集线器。 系统提供的 USB 集线器驱动程序为主机控制器支持的其他中心设备（如果有）注册此类的实例。

Microsoft Windows 驱动程序工具包 (WDK) 包含 [USBVIEW 示例应用程序](/samples/browse/)。 USBVIEW 示例使用过时的标识符 [**GUID_CLASS_USBHUB**](guid-class-usbhub.md) 向此设备接口类的实例通知。

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


[**GUID_CLASS_USBHUB**](guid-class-usbhub.md)

[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

[**GUID_DEVINTERFACE_USB_HOST_CONTROLLER**](guid-devinterface-usb-host-controller.md)


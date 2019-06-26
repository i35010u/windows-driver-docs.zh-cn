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
ms.openlocfilehash: f7d2d1c7a27d3e021db02bbb495a05874efd58a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353790"
---
# <a name="guiddevinterfaceusbdevice"></a>GUID_DEVINTERFACE_USB_DEVICE


GUID_DEVINTERFACE_USB_DEVICE[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[USB 设备](https://docs.microsoft.com/windows-hardware/drivers/)，附加到的 USB 集线器。

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

在系统提供的 USB 集线器驱动程序注册 GUID_DEVINTERFACE_USB_DEVICE 通知系统和应用程序连接到的 USB 集线器的 USB 设备的状态的实例。

Microsoft Windows Driver Kit (WDK) 包括[USBVIEW 示例应用程序](https://go.microsoft.com/fwlink/p/?linkid=256205)。 USBVIEW 示例使用已过时的标识符[ **GUID_CLASS_USB_DEVICE** ](guid-class-usb-device.md)注册此设备接口类的实例到达接收通知。

包括通过使用 DEFINE_GUID 宏，声明一个 GUID 的所有标头之前，必须包含 initguid.h。

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
<td align="left">Usbiodef.h (包括 Usbiodef.h，initguid.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_CLASS_USB_DEVICE**](guid-class-usb-device.md)

[**GUID_DEVINTERFACE_USB_HOST_CONTROLLER**](guid-devinterface-usb-host-controller.md)

[**GUID_DEVINTERFACE_USB_HUB**](guid-devinterface-usb-hub.md)

 

 







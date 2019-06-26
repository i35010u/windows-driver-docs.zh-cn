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
ms.openlocfilehash: ed4ac5d10ebfe13172c9b482020ec78e7a4da1ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386423"
---
# <a name="guiddevinterfaceusbhostcontroller"></a>GUID_DEVINTERFACE_USB_HOST_CONTROLLER


GUID_DEVINTERFACE_USB_HOST_CONTROLLER[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[USB](https://docs.microsoft.com/windows-hardware/drivers/)托管控制器设备。

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

USB 主控制器的系统提供的端口驱动程序注册的 GUID_DEVINTERFACE_USB_HOST_CONTROLLER 通知操作系统和应用程序存在 USB 主控制器的实例。

Microsoft Windows Driver Kit (WDK) 包括[USBVIEW 示例应用程序](https://go.microsoft.com/fwlink/p/?linkid=256205)。 使用已过时的标识符，USBVIEW [ **GUID_CLASS_USB_HOST_CONTROLLER** ](guid-class-usb-host-controller.md)枚举此设备接口类的实例。

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


[**GUID_CLASS_USB_HOST_CONTROLLER**](guid-class-usb-host-controller.md)

[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

[**GUID_DEVINTERFACE_USB_HUB**](guid-devinterface-usb-hub.md)

 

 







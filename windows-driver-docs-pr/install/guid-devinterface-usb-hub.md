---
title: GUID_DEVINTERFACE_USB_HUB
description: GUID_DEVINTERFACE_USB_HUB
ms.assetid: 899b77ad-fa98-4078-9207-69b422e3d0d0
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
ms.openlocfilehash: efe4f349f7857426f0c803727bd93ef64199629c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576218"
---
# <a name="guiddevinterfaceusbhub"></a>GUID_DEVINTERFACE_USB_HUB


GUID_DEVINTERFACE_USB_HUB[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930) hub 设备。

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

系统提供的 USB 端口驱动程序注册 GUID_DEVINTERFACE_USB_HUB 通知操作系统和应用程序的主机控制器设备的根中心存在的实例。 如果任何由主机控制器支持，在系统提供的 USB 集线器驱动程序注册其他中心的设备，此类的实例。

Microsoft Windows Driver Kit (WDK) 包括[USBVIEW 示例应用程序](https://go.microsoft.com/fwlink/p/?linkid=256205)。 USBVIEW 示例使用已过时的标识符[ **GUID_CLASS_USBHUB** ](guid-class-usbhub.md)接收此设备接口类的实例的通知。

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


[**GUID_CLASS_USBHUB**](guid-class-usbhub.md)

[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

[**GUID_DEVINTERFACE_USB_HOST_CONTROLLER**](guid-devinterface-usb-host-controller.md)

 

 







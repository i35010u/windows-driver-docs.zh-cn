---
title: GUID_CLASS_USB_DEVICE
description: GUID_CLASS_USB_DEVICE
ms.assetid: e014f3d5-541d-4e86-a572-b110ec5a822d
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
ms.openlocfilehash: 94981e59cd11e152cd201aaab1b4032290fac0f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348235"
---
# <a name="guidclassusbdevice"></a>GUID_CLASS_USB_DEVICE


GUID_CLASS_USB_DEVICE 是已过时标识符[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)有关[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)附加到的 USB 集线器的设备。 从 Microsoft Windows 2000 开始，使用[ **GUID_DEVINTERFACE_USB_DEVICE** ](guid-devinterface-usb-device.md)此类的新实例的类标识符。

<a name="remarks"></a>备注
-------

Microsoft Windows Driver Kit (WDK) 包括[USBVIEW 示例应用程序](https://go.microsoft.com/fwlink/p/?linkid=256205)。 USBVIEW 示例使用 GUID_CLASS_USB_DEVICE 进行注册，以通知 GUID_CLASS_USB_DEVICE 接口类的实例是否存在。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>已过时。 从 Windows 2000 开始，请改用 GUID_DEVINTERFACE_USB_DEVICE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Usbiodef.h （包括 Usbiodef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_USB_DEVICE**](guid-devinterface-usb-device.md)

 

 







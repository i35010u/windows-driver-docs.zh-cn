---
title: GUID_CLASS_USBHUB
description: GUID_CLASS_USBHUB
ms.assetid: 77232e67-9c8d-4054-b020-2739457d678d
keywords:
- GUID_CLASS_USBHUB 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_CLASS_USBHUB
api_location:
- Usbiodef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3c0a744a32d6e8d75d92467906916adadb1af043
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732995"
---
# <a name="guid_class_usbhub"></a>GUID_CLASS_USBHUB


GUID_CLASS_USBHUB 是[USB](../index.yml)集线器设备的[设备接口类](./overview-of-device-interface-classes.md)的过时标识符。 从 Microsoft Windows 2000 开始，使用此类的新实例 [**GUID_DEVINTERFACE_USB_HUB**](guid-devinterface-usb-hub.md) 类标识符。

<a name="remarks"></a>备注
-------

Microsoft Windows 驱动程序工具包 (WDK) 包含 [USBVIEW 示例应用程序](/samples/browse/)。 如果存在 GUID_CLASS_USBHUB 设备接口类的实例，则 USBVIEW 示例使用 GUID_CLASS_USBHUB 进行通知。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_USB_HUB。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Usbiodef (包含 Usbiodef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_USB_HUB**](guid-devinterface-usb-hub.md)


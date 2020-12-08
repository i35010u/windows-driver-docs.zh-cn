---
title: GUID_CLASS_MOUSE
description: GUID_CLASS_MOUSE
keywords:
- GUID_CLASS_MOUSE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_CLASS_MOUSE
api_location:
- Ntddmou.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b78aa2395e615d99c08e0aaee4da2ef442cbfd5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796103"
---
# <a name="guid_class_mouse"></a>GUID_CLASS_MOUSE


GUID_CLASS_MOUSE 是用于鼠标设备的 [设备接口类](./overview-of-device-interface-classes.md) 的过时标识符。 从 Microsoft Windows 2000 开始，使用此类的新实例 [**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md) 类标识符。

<a name="remarks"></a>备注
-------

WDK 中提供的 HID 示例包括鼠标类驱动程序。 鼠标类驱动程序使用 GUID_CLASS_MOUSE 来注册此设备接口类的实例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_MOUSE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddmou (包含 Ntddmou) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 


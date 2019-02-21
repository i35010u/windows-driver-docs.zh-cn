---
title: GUID_CLASS_MOUSE
description: GUID_CLASS_MOUSE
ms.assetid: 3b6578c7-0462-4fff-bd09-b9c768676ceb
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
ms.openlocfilehash: f0bbd499bd7af241e178e0c6ef055aecc6a854ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520294"
---
# <a name="guidclassmouse"></a>GUID_CLASS_MOUSE


GUID_CLASS_MOUSE 是已过时标识符[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)的鼠标设备。 从 Microsoft Windows 2000 开始，使用[ **GUID_DEVINTERFACE_MOUSE** ](guid-devinterface-mouse.md)此类的新实例的类标识符。

<a name="remarks"></a>备注
-------

WDK 中提供的 HID 示例包括鼠标类驱动程序。 鼠标类驱动程序使用 GUID_CLASS_MOUSE 注册此设备接口类的实例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，请改用 GUID_DEVINTERFACE_MOUSE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddmou.h （包括 Ntddmou.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 

 







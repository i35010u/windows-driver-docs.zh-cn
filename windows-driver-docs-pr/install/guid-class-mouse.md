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
ms.openlocfilehash: da83a0bb1fa8cc162be74dc1869c60023b9109cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378045"
---
# <a name="guidclassmouse"></a>GUID_CLASS_MOUSE


GUID_CLASS_MOUSE 是已过时标识符[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)的鼠标设备。 从 Microsoft Windows 2000 开始，使用[ **GUID_DEVINTERFACE_MOUSE** ](guid-devinterface-mouse.md)此类的新实例的类标识符。

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
<td align="left"><p>Version</p></td>
<td align="left"><p>已过时。 从 Windows 2000 开始，请改用 GUID_DEVINTERFACE_MOUSE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddmou.h （包括 Ntddmou.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 

 







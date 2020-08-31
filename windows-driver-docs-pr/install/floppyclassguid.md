---
title: FloppyClassGuid
description: FloppyClassGuid
ms.assetid: 60811704-0a59-48b4-b9c6-baf6c0f8c1c2
keywords:
- FloppyClassGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- FloppyClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8f9aca0ed7f85d770e8d0daafee67d6769ab6851
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095511"
---
# <a name="floppyclassguid"></a>FloppyClassGuid


FloppyClassGuid 是适用于软盘[存储设备](../storage/index.md)的[设备接口类](./overview-of-device-interface-classes.md)的过时标识符。 启动 Microsoft Windows 2000，使用此类的新实例 [**GUID_DEVINTERFACE_FLOPPY**](guid-devinterface-floppy.md) 类标识符。

<a name="remarks"></a>备注
-------

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括使用 FloppyClassGuid 注册此设备接口类的实例的 [软盘驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256192) 示例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_FLOPPY。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_FLOPPY**](guid-devinterface-floppy.md)

 


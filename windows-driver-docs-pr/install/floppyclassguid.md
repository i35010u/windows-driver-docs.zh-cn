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
ms.openlocfilehash: 7193165253053bba8b8691ef5a5689ff775f7db3
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732542"
---
# <a name="floppyclassguid"></a>FloppyClassGuid


FloppyClassGuid 是适用于软盘[存储设备](../storage/index.md)的[设备接口类](./overview-of-device-interface-classes.md)的过时标识符。 启动 Microsoft Windows 2000，使用此类的新实例 [**GUID_DEVINTERFACE_FLOPPY**](guid-devinterface-floppy.md) 类标识符。

<a name="remarks"></a>备注
-------

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括使用 FloppyClassGuid 注册此设备接口类的实例的 [软盘驱动程序](/samples/browse/) 示例。

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


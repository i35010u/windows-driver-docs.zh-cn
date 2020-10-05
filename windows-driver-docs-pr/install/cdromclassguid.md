---
title: CdRomClassGuid
description: CdRomClassGuid
ms.assetid: 406c28c9-8ef3-4ccc-bb70-a13b8d1ad64e
keywords:
- CdRomClassGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- CdRomClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fb988ba12f275edeb759baac575d1a22dba59ccd
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734268"
---
# <a name="cdromclassguid"></a>CdRomClassGuid


CdRomClassGuid 是 cd-rom[存储设备](../storage/index.md)的[设备接口类](./overview-of-device-interface-classes.md)的过时标识符。 从 Microsoft Windows 2000 开始，使用此类的新实例 [**GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md) 类标识符。

<a name="remarks"></a>备注
-------

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括 [CDROM 类驱动程序](/samples/browse/) 示例和 [Addfilter 存储筛选器工具](/samples/browse/)。 CDROM 类驱动程序示例使用 CdRomClassGuid 来注册 GUID_DEVINTERFACE_CDROM 设备接口类的实例。 示例 Addfilter 应用程序使用 CdRomClassGuid 来枚举 GUID_DEVINTERFACE_CDROM 设备接口类的实例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_CDROM。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md)


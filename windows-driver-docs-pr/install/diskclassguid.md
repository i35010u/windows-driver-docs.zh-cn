---
title: DiskClassGuid
description: DiskClassGuid
ms.assetid: eeefc86c-caff-4d1c-b2c1-aefde3bd21ed
keywords:
- DiskClassGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DiskClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 506214195909441c483eb889e2631163c7fc692e
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733523"
---
# <a name="diskclassguid"></a>DiskClassGuid


DiskClassGuid 是硬盘 [存储设备](../storage/index.md)的设备接口类的过时标识符。 从 Microsoft Windows 2000 开始，使用此类的新实例 [**GUID_DEVINTERFACE_DISK**](guid-devinterface-disk.md) 类标识符。

<a name="remarks"></a>备注
-------

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括 [磁盘类驱动程序](/samples/browse/) 示例和 [Addfilter 存储筛选器工具](/samples/browse/)。 Disk class driver 示例使用 DiskClassGuid 来注册 GUID_DEVINTERFACE_DISK 设备接口类的实例。 示例 Addfilter 应用程序使用 DiskClassGuid 来枚举 GUID_DEVINTERFACE_DISK 设备接口类的实例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_DISK。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_DISK**](guid-devinterface-disk.md)


---
title: GUID_DEVINTERFACE_CDROM
description: GUID_DEVINTERFACE_CDROM
keywords:
- GUID_DEVINTERFACE_CDROM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_CDROM
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0bb702b8858aeca7907d2ddd50271077c815acf5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789837"
---
# <a name="guid_devinterface_cdrom"></a>GUID_DEVINTERFACE_CDROM


为 cd-rom[存储设备](../storage/index.md)定义 GUID_DEVINTERFACE_CDROM[设备接口类](./overview-of-device-interface-classes.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_DEVINTERFACE_CDROM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F56308-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统为 CD-ROM 存储设备提供的类驱动程序将注册此设备接口类的实例，以通知操作系统和应用程序是否存在 CD-ROM 设备。

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括 [CDROM 类驱动程序](/samples/browse/) 示例和 [Addfilter 存储筛选器工具](/samples/browse/)。 Cd-rom 类驱动程序示例使用过时的标识符 [**CdRomClassGuid**](cdromclassguid.md) 来注册 GUID_DEVINTERFACE_CDROM 设备接口类的实例。 示例 Addfilter 应用程序使用 CdRomClassGuid 来枚举 GUID_DEVINTERFACE_CDROM 设备接口类的实例。

有关 CD-ROM 转换器设备的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_CDCHANGER**](guid-devinterface-cdchanger.md)。

有关存储设备的信息，请参阅 [存储驱动程序](../storage/storage-drivers.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**CdRomClassGuid**](cdromclassguid.md)

[**GUID_DEVINTERFACE_CDCHANGER**](guid-devinterface-cdchanger.md)


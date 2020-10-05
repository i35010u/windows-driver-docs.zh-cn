---
title: GUID_DEVINTERFACE_CDROM
description: GUID_DEVINTERFACE_CDROM
ms.assetid: ecc31c09-27f5-4a80-8aa6-adc70d8a76c3
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
ms.openlocfilehash: f7def053ea10cc9dd32cf844412213ad1de95d00
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732633"
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
<th align="left">属性</th>
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

## <a name="see-also"></a>另请参阅


[**CdRomClassGuid**](cdromclassguid.md)

[**GUID_DEVINTERFACE_CDCHANGER**](guid-devinterface-cdchanger.md)


---
title: GUID_DEVINTERFACE_CDCHANGER
description: GUID_DEVINTERFACE_CDCHANGER
keywords:
- GUID_DEVINTERFACE_CDCHANGER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_CDCHANGER
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dcc51cb2dde6fe9be6667591595f6a6ce8840928
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813133"
---
# <a name="guid_devinterface_cdchanger"></a>GUID_DEVINTERFACE_CDCHANGER


为 CD-ROM 转换器设备定义 GUID_DEVINTERFACE_CDCHANGER [设备接口类](./overview-of-device-interface-classes.md) 。

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
<td align="left"><p>GUID_DEVINTERFACE_CDCHANGER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F56312-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的 CD-ROM [更换器驱动程序](../storage/changer-drivers.md) 将注册 GUID_DEVINTERFACE_CDCHANGER 的实例，通知操作系统和应用程序是否存在 cd-rom 转换器设备。

有关 CD-ROM 设备的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md)。

有关存储设备的信息，请参阅 [存储驱动程序](../storage/storage-drivers.md)。

[**CdChangerClassGuid**](cdchangerclassguid.md) 是 GUID_DEVINTERFACE_CDCHANGER 设备接口类的过时标识符;对于此类的新实例，请改用 GUID_DEVINTERFACE_CDCHANGER。

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
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**CdChangerClassGuid**](cdchangerclassguid.md)

[**GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md)

 


---
title: GUID_DEVINTERFACE_CDCHANGER
description: GUID_DEVINTERFACE_CDCHANGER
ms.assetid: 9bcbe3d5-2057-44cb-a495-6edee14a9cbb
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
ms.openlocfilehash: 4d03d2e56316793ec8758c944a8b9c68133e84bb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370959"
---
# <a name="guiddevinterfacecdchanger"></a>GUID_DEVINTERFACE_CDCHANGER


GUID_DEVINTERFACE_CDCHANGER[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为 CD-ROM 换带机设备定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
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

系统提供 CD-ROM[更换器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/changer-drivers)注册 GUID_DEVINTERFACE_CDCHANGER 通知操作系统和应用程序的 CD-ROM 换带机设备是否存在的实例。

有关 CD-ROM 设备的设备接口类的信息，请参阅[ **GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md)。

有关存储设备的信息，请参阅[存储设备驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)。

[**CdChangerClassGuid** ](cdchangerclassguid.md)对于此类的新实例，而是使用 GUID_DEVINTERFACE_CDCHANGER 是 GUID_DEVINTERFACE_CDCHANGER 设备接口类; 的已过时标识符。

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
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h （包括 Ntddstor.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**CdChangerClassGuid**](cdchangerclassguid.md)

[**GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md)

 

 







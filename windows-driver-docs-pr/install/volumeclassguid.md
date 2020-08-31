---
title: VolumeClassGuid
description: VolumeClassGuid
ms.assetid: 30d0db03-fbea-4245-b8d7-ca3a06a54861
keywords:
- VolumeClassGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- VolumeClassGuid
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 497b3c49a7d032a439763bc40d1dc4e54ba08fdb
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094813"
---
# <a name="volumeclassguid"></a>VolumeClassGuid


VolumeClassGuid 是卷设备的 [设备接口类](./overview-of-device-interface-classes.md) 的过时标识符。 从 Microsoft Windows 2000 开始，使用此类的新实例 [**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md) 类标识符。

<a name="remarks"></a>备注
-------

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括一个 [Addfilter 存储筛选器工具](https://go.microsoft.com/fwlink/p/?linkid=256076) ，该工具使用 VolumeClassGuid 枚举 [**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md) 设备接口类的实例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，改用 GUID_DEVINTERFACE_VOLUME。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)

 


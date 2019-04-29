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
ms.openlocfilehash: 91a246f2734fc1d4d118ef26015a2ae4eaa79d1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358001"
---
# <a name="cdromclassguid"></a>CdRomClassGuid


CdRomClassGuid 是已过时标识符[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)cd-rom[存储设备](https://msdn.microsoft.com/library/windows/hardware/ff566969)。 从 Microsoft Windows 2000 开始，使用[ **GUID_DEVINTERFACE_CDROM** ](guid-devinterface-cdrom.md)此类的新实例的类标识符。

<a name="remarks"></a>备注
-------

存储[示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK 中包括[CDROM 类驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256093)示例并[Addfilter 存储筛选器工具](https://go.microsoft.com/fwlink/p/?linkid=256076)。 CDROM 类驱动程序示例使用 CdRomClassGuid 注册 GUID_DEVINTERFACE_CDROM 设备接口类的实例。 示例 Addfilter 应用程序使用 CdRomClassGuid 枚举 GUID_DEVINTERFACE_CDROM 设备接口类的实例。

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
<td align="left"><p>已过时。 从 Windows 2000 开始，请改用 GUID_DEVINTERFACE_CDROM。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h （包括 Ntddstor.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_CDROM**](guid-devinterface-cdrom.md)

 

 







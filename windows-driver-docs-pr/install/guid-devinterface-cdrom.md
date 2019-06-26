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
ms.openlocfilehash: bf8e3c75144eda4b84e05af890107e8a6241243f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372731"
---
# <a name="guiddevinterfacecdrom"></a>GUID_DEVINTERFACE_CDROM


GUID_DEVINTERFACE_CDROM[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)定义的 CD-ROM[存储设备](https://docs.microsoft.com/windows-hardware/drivers/storage/index)。

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

CD-ROM 存储设备的系统提供的类驱动程序注册通知的操作系统和应用程序的 CD-ROM 设备存在此设备接口类的实例。

存储[示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK 中包括[CDROM 类驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256093)示例并[Addfilter 存储筛选器工具](https://go.microsoft.com/fwlink/p/?linkid=256076)。 CD-ROM 类驱动程序示例使用已过时的标识符[ **CdRomClassGuid** ](cdromclassguid.md)注册 GUID_DEVINTERFACE_CDROM 设备接口类的实例。 示例 Addfilter 应用程序使用 CdRomClassGuid 枚举 GUID_DEVINTERFACE_CDROM 设备接口类的实例。

有关 CD-ROM 换带机设备的设备接口类的信息，请参阅[ **GUID_DEVINTERFACE_CDCHANGER**](guid-devinterface-cdchanger.md)。

有关存储设备的信息，请参阅[存储设备驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h （包括 Ntddstor.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**CdRomClassGuid**](cdromclassguid.md)

[**GUID_DEVINTERFACE_CDCHANGER**](guid-devinterface-cdchanger.md)

 

 







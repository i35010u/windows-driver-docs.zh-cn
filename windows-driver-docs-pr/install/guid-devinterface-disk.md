---
title: GUID_DEVINTERFACE_DISK
description: GUID_DEVINTERFACE_DISK
ms.assetid: 47782789-4504-4705-8c32-4d2bc508a7e2
keywords:
- GUID_DEVINTERFACE_DISK 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_DISK
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e0a383109c8dcbf7fffd3b1e27c3b3d3d1ab547e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372715"
---
# <a name="guiddevinterfacedisk"></a>GUID_DEVINTERFACE_DISK


GUID_DEVINTERFACE_DISK[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)定义为硬盘[存储设备](https://docs.microsoft.com/windows-hardware/drivers/storage/index)。

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
<td align="left"><p>GUID_DEVINTERFACE_DISK</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F56307-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的存储类驱动程序注册为磁盘存储设备的 GUID_DEVINTERFACE_DISK 实例。

存储[示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK 中包括[磁盘类驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256103)示例并[Addfilter 存储筛选器工具](https://go.microsoft.com/fwlink/p/?linkid=256076)。 磁盘类驱动程序示例使用已过时的标识符[ **DiskClassGuid** ](diskclassguid.md)注册 GUID_DEVINTERFACE_DISK 设备接口类的实例。 示例 Addfilter 应用程序使用 DiskClassGuid 枚举 GUID_DEVINTERFACE_DISK 设备接口类的实例。

存储驱动程序有关的信息，请参阅[存储设备驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)。

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


[**DiskClassGuid**](diskclassguid.md)

 

 







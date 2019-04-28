---
title: GUID_DEVINTERFACE_FLOPPY
description: GUID_DEVINTERFACE_FLOPPY
ms.assetid: 07d47168-a179-40ef-843b-c1efa6acb395
keywords:
- GUID_DEVINTERFACE_FLOPPY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_FLOPPY
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2816980d0a469f18048dda8769254b3be7a4c049
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342315"
---
# <a name="guiddevinterfacefloppy"></a>GUID_DEVINTERFACE_FLOPPY


GUID_DEVINTERFACE_FLOPPY[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)定义为软盘[存储设备](https://msdn.microsoft.com/library/windows/hardware/ff566969)。

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
<td align="left"><p>GUID_DEVINTERFACE_FLOPPY</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F56311-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

软盘存储设备的系统提供的存储类驱动程序注册为软盘存储设备的 GUID_DEVINTERFACE_FLOPPY 实例。

存储[示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK 中包括[软盘驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256192)此示例使用已过时的标识符[ **FloppyClassGuid** ](floppyclassguid.md)到注册 GUID_DEVINTERFACE_FLOPPY 设备接口类的实例。

存储驱动程序有关的信息，请参阅[存储设备驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566976)。

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


[**FloppyClassGuid**](floppyclassguid.md)

 

 







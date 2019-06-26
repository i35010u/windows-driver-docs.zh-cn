---
title: GUID_DEVINTERFACE_TAPE
description: GUID_DEVINTERFACE_TAPE
ms.assetid: af19bdf6-5205-4fc1-842f-081e34ea2337
keywords:
- GUID_DEVINTERFACE_TAPE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_TAPE
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dd9fd6a1352624fb56b3dd2fafd0d5d5b2755b37
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386420"
---
# <a name="guiddevinterfacetape"></a>GUID_DEVINTERFACE_TAPE


GUID_DEVINTERFACE_TAPE[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为磁带定义[存储设备](https://docs.microsoft.com/windows-hardware/drivers/storage/index)。

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
<td align="left"><p>GUID_DEVINTERFACE_TAPE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F5630B-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[磁带类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/tape-drivers)注册 GUID_DEVINTERFACE_TAPE 通知操作系统和应用程序的磁带存储设备状态的实例。

有关存储驱动程序的详细信息，请参阅[存储设备驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)。

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


[**TapeClassGuid**](tapeclassguid.md)

 

 







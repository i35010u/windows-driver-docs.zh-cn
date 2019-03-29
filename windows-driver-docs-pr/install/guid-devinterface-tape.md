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
ms.openlocfilehash: 2abd46d4145958c2a1aed807e71359413c069499
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568066"
---
# <a name="guiddevinterfacetape"></a>GUID_DEVINTERFACE_TAPE


GUID_DEVINTERFACE_TAPE[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为磁带定义[存储设备](https://msdn.microsoft.com/library/windows/hardware/ff566969)。

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

系统提供[磁带类驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff567961)注册 GUID_DEVINTERFACE_TAPE 通知操作系统和应用程序的磁带存储设备状态的实例。

有关存储驱动程序的详细信息，请参阅[存储设备驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566976)。

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

 

 







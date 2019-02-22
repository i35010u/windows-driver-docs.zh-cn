---
title: GUID_DEVINTERFACE_PARTITION
description: GUID_DEVINTERFACE_PARTITION
ms.assetid: c489b62a-167d-47a9-bfeb-fdd40cc8dece
keywords:
- GUID_DEVINTERFACE_PARTITION 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_PARTITION
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8ae3d375364af04c44885430f53ea11c30213b9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524562"
---
# <a name="guiddevinterfacepartition"></a>GUID_DEVINTERFACE_PARTITION


GUID_DEVINTERFACE_PARTITION[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为分区的设备定义。

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
<td align="left"><p>GUID_DEVINTERFACE_PARTITION</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F5630A-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供[存储设备驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566976)注册的是子设备分区实例 GUID_DEVINTERFACE_PARTITION[存储设备](https://msdn.microsoft.com/library/windows/hardware/ff566969)。

[**PartitionClassGuid** ](partitionclassguid.md) GUID_DEVINTERFACE_PARTITION 设备接口类的已过时标识符。 对于此类的新实例，请改为使用 GUID_DEVINTERFACE_PARTITION。

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
<td align="left">Ntddstor.h （包括 Ntddstor.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**PartitionClassGuid**](partitionclassguid.md)

 

 







---
title: GUID_DEVINTERFACE_STORAGEPORT
description: GUID_DEVINTERFACE_STORAGEPORT
ms.assetid: 58146169-102b-4355-82d0-ea60979bf901
keywords:
- GUID_DEVINTERFACE_STORAGEPORT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_STORAGEPORT
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9754d9d9b8fb44fe31ff04119b4d7b91566c2b23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383204"
---
# <a name="guiddevinterfacestorageport"></a>GUID_DEVINTERFACE_STORAGEPORT


GUID_DEVINTERFACE_STORAGEPORT[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[存储端口设备](https://msdn.microsoft.com/library/windows/hardware/ff566994)。

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
<td align="left"><p>GUID_DEVINTERFACE_STORAGEPORT</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{2ACCFE60-C130-11D2-B082-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的驱动程序存储端口设备注册 GUID_DEVINTERFACE_STORAGEPORT 通知操作系统和应用程序的存储设备适配器存在的实例。

有关存储驱动程序的详细信息，请参阅[存储设备驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566976)。

[**StoragePortClassGuid** ](storageportclassguid.md) GUID_DEVINTERFACE_STORAGEPORT 设备接口类的已过时标识符。 对于此类的新实例，请改为使用 GUID_DEVINTERFACE_STORAGEPORT。

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


[**StoragePortClassGuid**](storageportclassguid.md)

 

 







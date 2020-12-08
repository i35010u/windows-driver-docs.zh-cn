---
title: GUID_DEVINTERFACE_TAPE
description: GUID_DEVINTERFACE_TAPE
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
ms.openlocfilehash: 89bc6f304a9a59fc536f9dd2bd3974ed2a3b89ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830421"
---
# <a name="guid_devinterface_tape"></a>GUID_DEVINTERFACE_TAPE


为磁带[存储设备](../storage/index.md)定义 GUID_DEVINTERFACE_TAPE[设备接口类](./overview-of-device-interface-classes.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
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

系统提供的 [磁带类驱动程序](../storage/tape-drivers-overview.md) 将注册 GUID_DEVINTERFACE_TAPE 的实例，以通知操作系统和应用程序是否存在磁带存储设备。

有关存储驱动程序的详细信息，请参阅 [存储驱动程序](../storage/storage-drivers.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**TapeClassGuid**](tapeclassguid.md)


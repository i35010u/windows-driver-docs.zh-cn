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
ms.openlocfilehash: 01bde05c59322db65b99d5a3e46b68d4a89fe7b9
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096901"
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

系统提供的 [磁带类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/tape-drivers) 将注册 GUID_DEVINTERFACE_TAPE 的实例，以通知操作系统和应用程序是否存在磁带存储设备。

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

## <a name="see-also"></a>另请参阅


[**TapeClassGuid**](tapeclassguid.md)

 


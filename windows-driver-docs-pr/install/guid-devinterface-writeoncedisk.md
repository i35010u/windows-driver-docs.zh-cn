---
title: GUID_DEVINTERFACE_WRITEONCEDISK
description: GUID_DEVINTERFACE_WRITEONCEDISK
keywords:
- GUID_DEVINTERFACE_WRITEONCEDISK 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_WRITEONCEDISK
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3e32155bfed90d14aec4fd3b252d8da1dd1cd09f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808163"
---
# <a name="guid_devinterface_writeoncedisk"></a>GUID_DEVINTERFACE_WRITEONCEDISK


为一次性写入磁盘设备定义了 GUID_DEVINTERFACE_WRITEONCEDISK [设备接口类](./overview-of-device-interface-classes.md) 。

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
<td align="left"><p>GUID_DEVINTERFACE_WRITEONCEDISK</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F5630C-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的 [存储驱动程序](../storage/storage-drivers.md) 将 GUID_DEVINTERFACE_WRITEONCEDISK 的实例注册，通知操作系统和应用程序是否存在写入一次写入的磁盘，例如 cd-r。

[**WriteOnceDiskClassGuid**](writeoncediskclassguid.md) 是 GUID_DEVINTERFACE_WRITEONCEDISK 设备接口类的过时标识符。 对于此类的新实例，请改用 GUID_DEVINTERFACE_WRITEONCEDISK。

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
<td align="left">Ntddstor (包含 Ntddstor) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WriteOnceDiskClassGuid**](writeoncediskclassguid.md)

 


---
title: GUID_DEVINTERFACE_DISK
description: GUID_DEVINTERFACE_DISK
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
ms.openlocfilehash: b11ceb20c015de2182059643670812b5ad87415c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790601"
---
# <a name="guid_devinterface_disk"></a>GUID_DEVINTERFACE_DISK


为硬盘[存储设备](../storage/index.md)定义 GUID_DEVINTERFACE_DISK[设备接口类](./overview-of-device-interface-classes.md)。

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

系统提供的存储类驱动程序为硬盘存储设备注册 GUID_DEVINTERFACE_DISK 的实例。

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括 [磁盘类驱动程序](/samples/browse/) 示例和 [Addfilter 存储筛选器工具](/samples/browse/)。 磁盘类驱动程序示例使用过时的标识符 [**DiskClassGuid**](diskclassguid.md) 来注册 GUID_DEVINTERFACE_DISK 设备接口类的实例。 示例 Addfilter 应用程序使用 DiskClassGuid 来枚举 GUID_DEVINTERFACE_DISK 设备接口类的实例。

有关存储驱动程序的信息，请参阅 [存储驱动程序](../storage/storage-drivers.md)。

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


[**DiskClassGuid**](diskclassguid.md)


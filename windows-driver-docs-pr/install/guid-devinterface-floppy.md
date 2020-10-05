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
ms.openlocfilehash: 75ed116ea9840383f214a4efa5d3c4f5edc4fe17
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732849"
---
# <a name="guid_devinterface_floppy"></a>GUID_DEVINTERFACE_FLOPPY


为软盘[存储设备](../storage/index.md)定义了 GUID_DEVINTERFACE_FLOPPY[设备接口类](./overview-of-device-interface-classes.md)。

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

适用于软盘存储设备的系统提供的存储类驱动程序为软盘存储设备注册 GUID_DEVINTERFACE_FLOPPY 的实例。

WDK 中的存储[示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)包括使用过时的标识符[**FloppyClassGuid**](floppyclassguid.md)注册 GUID_DEVINTERFACE_FLOPPY 设备接口类的实例的[软盘驱动程序](/samples/browse/)示例。

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

## <a name="see-also"></a>另请参阅


[**FloppyClassGuid**](floppyclassguid.md)


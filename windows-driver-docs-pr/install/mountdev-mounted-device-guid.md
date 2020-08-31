---
title: MOUNTDEV_MOUNTED_DEVICE_GUID
description: MOUNTDEV_MOUNTED_DEVICE_GUID
ms.assetid: 48d127ed-414b-40bb-8a35-6472c8783b81
keywords:
- MOUNTDEV_MOUNTED_DEVICE_GUID 设备和驱动程序安装
topic_type:
- apiref
api_name:
- MOUNTDEV_MOUNTED_DEVICE_GUID
api_location:
- Mountmgr.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b65a6acee5bfb74460d791fe55d2ecbb52492c98
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095005"
---
# <a name="mountdev_mounted_device_guid"></a>MOUNTDEV_MOUNTED_DEVICE_GUID


为卷设备定义 MOUNTDEV_MOUNTED_DEVICE_GUID [设备接口类](./overview-of-device-interface-classes.md) 。

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
<td align="left"><p>MOUNTDEV_MOUNTED_DEVICE_GUID</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F5630D-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此设备接口类的 MOUNTDEV_MOUNTED_DEVICE_GUID 标识符是 [**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md) 设备接口类的别名。

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括 [ClassPnP 存储类驱动程序库，该程序库](https://go.microsoft.com/fwlink/p/?linkid=256095) 使用 MOUNTDEV_MOUNTED_DEVICE_GUID 来注册 GUID_DEVINTERFACE_VOLUME 设备接口类的实例。

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
<td align="left">Mountmgr (包含 Mountmgr) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)

 


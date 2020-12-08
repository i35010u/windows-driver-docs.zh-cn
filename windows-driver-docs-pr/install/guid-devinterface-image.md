---
title: GUID_DEVINTERFACE_IMAGE
description: GUID_DEVINTERFACE_IMAGE
keywords:
- GUID_DEVINTERFACE_IMAGE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_IMAGE
api_location:
- Wiaintfc.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e38f96552d187acfd9132122e4e1ac0f04147054
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789821"
---
# <a name="guid_devinterface_image"></a>GUID_DEVINTERFACE_IMAGE


GUID_DEVINTERFACE_IMAGE [设备接口类](./overview-of-device-interface-classes.md) 是为 WIA 设备定义的， [而) 设备的静止图像 (](../image/index.md)，包括数字照相机和扫描仪。

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
<td align="left"><p>GUID_DEVINTERFACE_IMAGE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{6BDD1FC6-810F-11D0-BEC7-08002BE2092F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统提供的用于 WIA 设备的内核模式驱动程序注册此设备接口类的实例，通知操作系统和应用程序是否存在 WIA 设备。

有关 WIA 驱动程序和 STI 驱动程序的信息，请参阅 [Windows 映像获取驱动程序](../image/windows-image-acquisition-drivers.md)。

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
<td align="left"><p>在 Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Wiaintfc (包含 Wiaintfc) </td>
</tr>
</tbody>
</table>

 


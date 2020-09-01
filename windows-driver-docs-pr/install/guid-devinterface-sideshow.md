---
title: GUID_DEVINTERFACE_SIDESHOW
description: GUID_DEVINTERFACE_SIDESHOW
ms.assetid: 74afef18-bfb3-457c-8112-29dadd0c7e66
keywords:
- GUID_DEVINTERFACE_SIDESHOW 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_SIDESHOW
api_location:
- WindowsSideShowDriverEvents.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 79e27a298e8e6b664f655e275bfd04d3f60e8da0
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096913"
---
# <a name="guid_devinterface_sideshow"></a>GUID_DEVINTERFACE_SIDESHOW


为[Windows 边栏显示设备](../index.yml)定义 GUID_DEVINTERFACE_SIDESHOW[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>GUID_DEVINTERFACE_SIDESHOW</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{152E5811-FEB9-4B00-90F4-D32947AE1681}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

适用于 Windows 边栏显示兼容设备的驱动程序将注册 GUID_DEVINTERFACE_SIDESHOW 的实例，以通知系统和应用程序是否存在 Windows 边栏显示设备。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Microsoft Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">WindowsSideShowDriverEvents (包含 WindowsSideShowDriverEvents) </td>
</tr>
</tbody>
</table>

 


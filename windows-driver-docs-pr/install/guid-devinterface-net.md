---
title: GUID_DEVINTERFACE_NET
description: GUID_DEVINTERFACE_NET
ms.assetid: e1cdda95-1915-4bbc-86e9-dff99b7fcc7b
keywords:
- GUID_DEVINTERFACE_NET 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_NET
api_location:
- Ndisguid.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c984b542c05117145d36013908afbb8ec53e7a85
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096937"
---
# <a name="guid_devinterface_net"></a>GUID_DEVINTERFACE_NET


为[网络设备](../network/index.md)定义 GUID_DEVINTERFACE_NET[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>GUID_DEVINTERFACE_NET</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{CAC88484-7515-4C03-82E6-71A87ABAC361}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

网络设备的驱动程序注册此设备接口类的实例，通知其他网络组件和应用程序是否存在网络设备。

NDIS 为 NDIS 微型端口驱动程序注册此接口类的实例。

有关网络设备和驱动程序的信息，请参阅 [网络设计指南](../network/index.md)。

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
<td align="left"><p>在 Windows Vista、Windows Server 2003 可伸缩网络包 (.SNP) 以及 Windows 的更高版本中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ndisguid (包含 Ndisguid) </td>
</tr>
</tbody>
</table>

 


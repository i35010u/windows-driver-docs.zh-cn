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
ms.openlocfilehash: 5970f5a734e17a9b59c3a4db9b163b89aa71c68e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363745"
---
# <a name="guiddevinterfacenet"></a>GUID_DEVINTERFACE_NET


GUID_DEVINTERFACE_NET[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[网络设备](https://msdn.microsoft.com/library/windows/hardware/ff568356)。

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

网络设备的驱动程序注册此设备接口类，以通知其他网络组件和网络设备的状态显示的应用程序的实例。

NDIS 注册 NDIS 微型端口驱动程序将此接口类的实例。

有关网络设备和驱动程序的信息，请参阅[网络设计指南](https://msdn.microsoft.com/library/windows/hardware/ff568356)。

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
<td align="left"><p>在 Windows Vista、 Windows Server 2003 可伸缩网络包 (SNP) 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ndisguid.h （包括 Ndisguid.h）</td>
</tr>
</tbody>
</table>

 

 






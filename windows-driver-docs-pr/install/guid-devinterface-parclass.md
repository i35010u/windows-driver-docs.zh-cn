---
title: GUID_DEVINTERFACE_PARCLASS
description: GUID_DEVINTERFACE_PARCLASS
keywords:
- GUID_DEVINTERFACE_PARCLASS 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_PARCLASS
api_location:
- Ntddpar.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0112b17e04261325279585c69d6fa97616cd72d5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805483"
---
# <a name="guid_devinterface_parclass"></a>GUID_DEVINTERFACE_PARCLASS


为附加到[并行端口](/previous-versions/ff544263(v=vs.85))的设备定义 GUID_DEVINTERFACE_PARCLASS[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>GUID_DEVINTERFACE_PARCLASS</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{811FC6A5-F728-11D0-A537-0000F8753ED1}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

连接到并行端口的并行设备的驱动程序将注册 GUID_DEVINTERFACE_PARCLASS 的实例，以通知操作系统和存在并行设备的应用程序。

系统提供的并行端口总线驱动程序为附加到并行端口的每个硬件设备创建此设备接口类的实例。

有关并行设备和驱动程序的信息，请参阅 [并行设备设计指南](/previous-versions/ff544263(v=vs.85))。

有关并行端口的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_PARALLEL**](guid-devinterface-parallel.md)。

[**GUID_PARCLASS_DEVICE**](guid-parclass-device.md) 是此设备接口类的过时标识符;对于此类的新实例，请改用 GUID_DEVINTERFACE_PARCLASS。

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
<td align="left">Ntddpar (包含 Ntddpar) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_PARALLEL**](guid-devinterface-parallel.md)

[**GUID_PARCLASS_DEVICE**](guid-parclass-device.md)

 


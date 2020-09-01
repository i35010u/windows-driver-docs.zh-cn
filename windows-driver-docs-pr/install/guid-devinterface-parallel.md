---
title: GUID_DEVINTERFACE_PARALLEL
description: GUID_DEVINTERFACE_PARALLEL
ms.assetid: 3c7c27ba-aad6-4ca5-ba26-fba206f967b9
keywords:
- GUID_DEVINTERFACE_PARALLEL 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_PARALLEL
api_location:
- Ntddpar.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a2a101a45db8719e6e75e8dc8dbc1dec25d0fd83
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096923"
---
# <a name="guid_devinterface_parallel"></a>GUID_DEVINTERFACE_PARALLEL


为支持 IEEE 1284 兼容硬件接口的[并行端口](/previous-versions/ff544263(v=vs.85))定义 GUID_DEVINTERFACE_PARALLEL[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>GUID_DEVINTERFACE_PARALLEL</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{97F76EF0-F883-11D0-AF1F-0000F800845C}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

并行端口驱动程序注册 GUID_DEVINTERFACE_PARALLEL 的实例，以通知操作系统和应用程序是否存在并行端口。

系统提供的并行端口函数驱动程序为并行端口注册此设备类的实例。

有关并行设备和驱动程序的信息，请参阅 [并行端口和设备简介](/previous-versions/ff543964(v=vs.85))。

有关连接到并行端口的设备的设备接口类的信息，请参阅 [**GUID_DEVINTERFACE_PARCLASS**](guid-devinterface-parclass.md)。

[**GUID_PARALLEL_DEVICE**](guid-parallel-device.md) 是此设备接口类的过时标识符;对于此类的新实例，请改用 GUID_DEVINTERFACE_PARALLEL。

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

## <a name="see-also"></a>另请参阅


[**GUID_DEVINTERFACE_PARCLASS**](guid-devinterface-parclass.md)

[**GUID_PARALLEL_DEVICE**](guid-parallel-device.md)

 


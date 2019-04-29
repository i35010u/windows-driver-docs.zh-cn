---
title: GUID_DEVINTERFACE_PARCLASS
description: GUID_DEVINTERFACE_PARCLASS
ms.assetid: d55195d4-f4f5-464f-a1ca-5fe0eafccb2a
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
ms.openlocfilehash: ab08bb06e662e97bc956d7d5dfca21228f4810fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363699"
---
# <a name="guiddevinterfaceparclass"></a>GUID_DEVINTERFACE_PARCLASS


GUID_DEVINTERFACE_PARCLASS[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)定义为附加到的设备[并行端口](https://msdn.microsoft.com/library/windows/hardware/ff544263)。

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

并行连接到并行端口的设备驱动程序注册 GUID_DEVINTERFACE_PARCLASS 通知操作系统和应用程序的并行设备存在的实例。

并行端口的系统提供的总线驱动程序创建每个硬件设备连接到并行端口将此设备接口类的实例。

有关并行的设备和驱动程序的信息，请参阅[并行设备设计指南](https://msdn.microsoft.com/library/windows/hardware/ff544263)。

有关并行端口设备接口类的信息，请参阅[ **GUID_DEVINTERFACE_PARALLEL**](guid-devinterface-parallel.md)。

[**GUID_PARCLASS_DEVICE** ](guid-parclass-device.md)对于此类的新实例，而是使用 GUID_DEVINTERFACE_PARCLASS 是此设备接口类; 的已过时标识符。

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
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddpar.h （包括 Ntddpar.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_PARALLEL**](guid-devinterface-parallel.md)

[**GUID_PARCLASS_DEVICE**](guid-parclass-device.md)

 

 







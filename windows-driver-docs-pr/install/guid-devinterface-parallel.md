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
ms.openlocfilehash: be309712967d427624c2e4ab59a4aaf0df719c1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363728"
---
# <a name="guiddevinterfaceparallel"></a>GUID_DEVINTERFACE_PARALLEL


GUID_DEVINTERFACE_PARALLEL[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[并行端口](https://msdn.microsoft.com/library/windows/hardware/ff544263)支持 IEEE 1284 兼容的硬件接口。

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

驱动程序的并行端口注册 GUID_DEVINTERFACE_PARALLEL 通知操作系统和应用程序的并行端口存在的实例。

并行端口的系统提供的函数驱动程序注册的并行端口此设备类的实例。

有关并行的设备和驱动程序的信息，请参阅[简介并行端口和设备](https://msdn.microsoft.com/library/windows/hardware/ff543964)。

有关附加到并行端口设备的设备接口类的信息，请参阅[ **GUID_DEVINTERFACE_PARCLASS**](guid-devinterface-parclass.md)。

[**GUID_PARALLEL_DEVICE** ](guid-parallel-device.md)对于此类的新实例，而是使用 GUID_DEVINTERFACE_PARALLEL 是此设备接口类; 的已过时标识符。

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


[**GUID_DEVINTERFACE_PARCLASS**](guid-devinterface-parclass.md)

[**GUID_PARALLEL_DEVICE**](guid-parallel-device.md)

 

 







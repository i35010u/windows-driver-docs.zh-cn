---
title: MPIOMoveDevice 函数
description: MPIOMoveDevice 方法用于在设备上设置活动的路径。
ms.assetid: aa3da461-ea55-4f60-b957-eb6b6cc3aeec
keywords:
- MPIOMoveDevice 函数存储设备
topic_type:
- apiref
api_name:
- MPIOMoveDevice
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d99804d6eb0aecdbf9d529ec0627f077c519538
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377470"
---
# <a name="mpiomovedevice-function"></a>MPIOMoveDevice 函数


MPIOMoveDevice 方法用于在设备上设置活动的路径。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void MPIOMoveDevice(
   [in, Description("MPIO Disk Ordinal"):amended] uint32    DiskOrdinal,
   [in, Description("Move Flags."):amended] uint32          Flags,
   [in, Description("PathID to set Active"):amended] uint64 PathID
);
```

<a name="parameters"></a>Parameters
----------

*DiskOrdinal*   
32-位域，指定 MPIO 磁盘序号值。

*标志*   
32-位域，指定与移动设备相关联的标志。

*PathID*   
64-位域，指定与设备相关联的路径。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MPIO\_WMI\_方法 WMI 类。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">MPIOwmi.h （包括 MPIOwmi.h）</td>
</tr>
</tbody>
</table>

 

 






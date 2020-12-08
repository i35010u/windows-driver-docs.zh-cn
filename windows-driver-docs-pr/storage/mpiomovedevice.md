---
title: MPIOMoveDevice 函数
description: MPIOMoveDevice 方法用于设置设备上的活动路径。
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
ms.openlocfilehash: 7141814c1818d0feaa7ee88c9f825c4f101a9e56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785593"
---
# <a name="mpiomovedevice-function"></a>MPIOMoveDevice 函数


MPIOMoveDevice 方法用于设置设备上的活动路径。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void MPIOMoveDevice(
   [in, Description("MPIO Disk Ordinal"):amended] uint32    DiskOrdinal,
   [in, Description("Move Flags."):amended] uint32          Flags,
   [in, Description("PathID to set Active"):amended] uint64 PathID
);
```

<a name="parameters"></a>参数
----------

*DiskOrdinal*   
指定 MPIO 磁盘序号值的32位域。

*随意*   
一个32位域，指定与设备移动关联的标志。

*PathID*   
指定与设备关联的路径的64位域。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MPIO \_ wmi \_ 方法 wmi 类。

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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">MPIOwmi (包含 MPIOwmi) </td>
</tr>
</tbody>
</table>

 

 






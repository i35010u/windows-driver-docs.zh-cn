---
title: ClearPathHealthCounters 函数
description: ClearPathHealthCounters 方法用于清除特定的 MPIO 磁盘路径的所有收集到的 MPIO 运行状况统计信息。
ms.assetid: 97f110c9-50c4-4570-ad5e-d1d17b711c6a
keywords:
- ClearPathHealthCounters 函数存储设备
topic_type:
- apiref
api_name:
- ClearPathHealthCounters
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bf3dafd907adb31d354a6fd7bb3a0fdc43fa538c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360928"
---
# <a name="clearpathhealthcounters-function"></a>ClearPathHealthCounters 函数


ClearPathHealthCounters 方法用于清除特定的 MPIO 磁盘路径的所有收集到的 MPIO 运行状况统计信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void ClearPathHealthCounters(
   [in, Description("64-bit Path Identifier"):amended] uint64 PathID
);
```

<a name="parameters"></a>Parameters
----------

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

 

 






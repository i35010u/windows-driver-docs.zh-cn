---
title: ClearMpioDiskHealthCounters 函数
description: ClearMpioDiskHealthCounters 方法用于清除的 MPIO 磁盘收集到的 MPIO 统计信息。
ms.assetid: 1ac415b2-87d4-430d-8713-a871c6af1006
keywords:
- ClearMpioDiskHealthCounters 函数存储设备
topic_type:
- apiref
api_name:
- ClearMpioDiskHealthCounters
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a44ed8a1d28bd03383d46b11421daedc737ccd1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540634"
---
# <a name="clearmpiodiskhealthcounters-function"></a>ClearMpioDiskHealthCounters 函数


ClearMpioDiskHealthCounters 方法用于清除的 MPIO 磁盘收集到的 MPIO 统计信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void ClearMpioDiskHealthCounters(
   [in, Description("MPIO Disk Ordinal"):amended] uint32 DiskOrdinal
);
```

<a name="parameters"></a>参数
----------

*DiskOrdinal*   
表示 MPIO 32-位域的磁盘的序号值。

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
<td align="left"><p>标头</p></td>
<td align="left">MPIOwmi.h （包括 MPIOwmi.h）</td>
</tr>
</tbody>
</table>

 

 






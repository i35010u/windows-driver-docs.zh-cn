---
title: ClearMpioDiskHealthCounters 函数
description: ClearMpioDiskHealthCounters 方法用于清除 MPIO 磁盘的已收集 MPIO 统计信息。
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
ms.openlocfilehash: 294869b007a19c9b0cb100586f6be267523b716e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811755"
---
# <a name="clearmpiodiskhealthcounters-function"></a>ClearMpioDiskHealthCounters 函数


ClearMpioDiskHealthCounters 方法用于清除 MPIO 磁盘的已收集 MPIO 统计信息。

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
表示 MPIO 磁盘序号值的32位域。

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

 

 






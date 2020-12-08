---
title: ClearPathHealthCounters 函数
description: ClearPathHealthCounters 方法用于清除 MPIO 磁盘的特定路径收集的所有 MPIO 运行状况统计信息。
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
ms.openlocfilehash: 8db5ce2fc993874ebe1cb229d0162e9e28a4f1ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804719"
---
# <a name="clearpathhealthcounters-function"></a>ClearPathHealthCounters 函数


ClearPathHealthCounters 方法用于清除 MPIO 磁盘的特定路径收集的所有 MPIO 运行状况统计信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void ClearPathHealthCounters(
   [in, Description("64-bit Path Identifier"):amended] uint64 PathID
);
```

<a name="parameters"></a>参数
----------

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

 

 






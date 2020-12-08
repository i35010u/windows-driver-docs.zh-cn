---
title: SetDSMCounters 函数
description: SetDSMCounters 方法用于设置特定 DSM 的计时器计数器。
keywords:
- SetDSMCounters 函数存储设备
topic_type:
- apiref
api_name:
- SetDSMCounters
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 986ebe573591694a8e6edf59a0c54232472fca15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782099"
---
# <a name="setdsmcounters-function"></a>SetDSMCounters 函数


SetDSMCounters 方法用于设置特定 DSM 的计时器计数器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SetDSMCounters(
   [in, Description("DSM Context"):amended] uint64              DSMcontext,
   [in, Description("DSM Timer Counters"):amended] DSM_COUNTERS DsmCounters
);
```

<a name="parameters"></a>参数
----------

*DSMcontext*   
提供 DSM 上下文的64位域。

*DsmCounters*   
DSM \_ 计数器结构。

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

 

 






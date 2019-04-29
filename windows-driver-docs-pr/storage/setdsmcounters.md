---
title: SetDSMCounters 函数
description: SetDSMCounters 方法用于设置计时器计数器，请为特定的 DSM。
ms.assetid: 6ea2ae07-d50e-48af-92da-7a5083a75bc7
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
ms.openlocfilehash: e08c7f773f9fa31352c1da62da982958219ec11a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358522"
---
# <a name="setdsmcounters-function"></a>SetDSMCounters 函数


SetDSMCounters 方法用于设置计时器计数器，请为特定的 DSM。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SetDSMCounters(
   [in, Description("DSM Context"):amended] uint64              DSMcontext,
   [in, Description("DSM Timer Counters"):amended] DSM_COUNTERS DsmCounters
);
```

<a name="parameters"></a>Parameters
----------

*DSMcontext*   
64-位域提供的 DSM 上下文。

*DsmCounters*   
DSM\_计数器结构。

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

 

 






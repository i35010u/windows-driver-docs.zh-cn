---
title: DsmSetLoadBalancePolicyALUA 函数
description: DsmSetLoadBalancePolicyALUA 方法用于设置 DSM ALUA 负载平衡策略。
ms.assetid: f63bdf0a-5b78-475d-b7c5-2af587b6356f
keywords:
- DsmSetLoadBalancePolicyALUA 函数存储设备
topic_type:
- apiref
api_name:
- DsmSetLoadBalancePolicyALUA
api_location:
- MPIOdisk.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5f81e6f48b1f28aedb580fe8381984c1fcffc950
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522725"
---
# <a name="dsmsetloadbalancepolicyalua-function"></a>DsmSetLoadBalancePolicyALUA 函数


**DsmSetLoadBalancePolicyALUA**方法用于设置 DSM ALUA 负载平衡策略。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void DsmSetLoadBalancePolicyALUA(
   [in, Description("New Load Balance policy to be set"):amended] DSM_Load_Balance_Policy_V2 LoadBalancePolicy,
   [out, Description("Status of the operation"):amended] uint32                              Status
);
```

<a name="parameters"></a>参数
----------

*LoadBalancePolicy*   
一个[ **DsmSetLoadBalancePolicyALUA\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff552675)结构。

*状态*   
操作的状态。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此 WMI 方法属于[DSM\_LB\_Operations](dsm-lb-operations-wmi-class.md) WMI 类。

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
<td align="left">MPIOdisk.h （包括 MPIOdisk.h）</td>
</tr>
</tbody>
</table>

 

 






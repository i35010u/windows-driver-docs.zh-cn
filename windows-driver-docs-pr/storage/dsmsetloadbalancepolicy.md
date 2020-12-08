---
title: DsmSetLoadBalancePolicy 函数
description: DsmSetLoadBalancePolicy 方法用于设置 DSM 负载平衡策略。
keywords:
- DsmSetLoadBalancePolicy 函数存储设备
topic_type:
- apiref
api_name:
- DsmSetLoadBalancePolicy
api_location:
- MPIOdisk.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d609f1b96b0fe5317561e9f2128368ba44336544
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835367"
---
# <a name="dsmsetloadbalancepolicy-function"></a>DsmSetLoadBalancePolicy 函数


**DsmSetLoadBalancePolicy** 方法用于设置 DSM 负载平衡策略。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void DsmSetLoadBalancePolicy(
   [in, Description("New Load Balance policy to be set"):amended] DSM_Load_Balance_Policy LoadBalancePolicy,
   [out, Description("Status of the operation"):amended] uint32                           Status
);
```

<a name="parameters"></a>参数
----------

*LoadBalancePolicy*   
[**DsmSetLoadBalancePolicy \_ OUT**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsmsetloadbalancepolicy_out)结构。

*状态*   
操作的状态。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此 WMI 方法属于 [DSM \_ LB \_ 操作](dsm-lb-operations-wmi-class.md) WMI 类。

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
<td align="left">MPIOdisk (包含 MPIOdisk) </td>
</tr>
</tbody>
</table>

 


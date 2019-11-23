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
ms.openlocfilehash: f7f75320262701266f584b9851e7344ce723d0a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844560"
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
[**DsmSetLoadBalancePolicyALUA\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsmsetloadbalancepolicyalua_out)结构。

*状态*   
操作的状态。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此 WMI 方法属于[DSM\_LB\_操作](dsm-lb-operations-wmi-class.md)WMI 类。

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
<td align="left">MPIOdisk （包括 MPIOdisk）</td>
</tr>
</tbody>
</table>

 

 






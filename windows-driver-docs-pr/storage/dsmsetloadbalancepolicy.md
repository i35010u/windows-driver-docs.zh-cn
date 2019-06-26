---
title: DsmSetLoadBalancePolicy 函数
description: DsmSetLoadBalancePolicy 方法用于设置 DSM 负载平衡策略。
ms.assetid: f53a776a-b350-4424-855a-49323587c57b
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
ms.openlocfilehash: e77d64da9d540cdefbe767f92af8041705e45c32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373212"
---
# <a name="dsmsetloadbalancepolicy-function"></a>DsmSetLoadBalancePolicy 函数


**DsmSetLoadBalancePolicy**方法用于设置 DSM 负载平衡策略。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void DsmSetLoadBalancePolicy(
   [in, Description("New Load Balance policy to be set"):amended] DSM_Load_Balance_Policy LoadBalancePolicy,
   [out, Description("Status of the operation"):amended] uint32                           Status
);
```

<a name="parameters"></a>Parameters
----------

*LoadBalancePolicy*   
一个[ **DsmSetLoadBalancePolicy\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_dsmsetloadbalancepolicy_out)结构。

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
<td align="left"><p>Header</p></td>
<td align="left">MPIOdisk.h （包括 MPIOdisk.h）</td>
</tr>
</tbody>
</table>

 

 






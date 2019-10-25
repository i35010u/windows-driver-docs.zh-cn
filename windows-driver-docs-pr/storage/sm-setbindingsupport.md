---
title: SM\_SetBindingSupport 函数
description: SM\_SetBindingSupport 方法设置所指示的端口的绑定功能。
ms.assetid: 31a37fa5-db3c-4944-bf93-e221fb42dc6d
keywords:
- SM_SetBindingSupport 函数存储设备
topic_type:
- apiref
api_name:
- SM_SetBindingSupport
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2ed744d8ccee6307cfdb1403f5cb3a0894ea600b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845450"
---
# <a name="sm_setbindingsupport-function"></a>SM\_SetBindingSupport 函数


SM\_SetBindingSupport 方法设置所指示的端口的绑定功能。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SetBindingSupport(
   [in, HBAType("HBA_WWN")] uint8                HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DomainPortWWN[8],
   [in, HBAType("SMHBA_BIND_CAPABILITY")] uint32 Flags,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
将检索其持久性绑定的端口的全球名称（WWN）。

*DomainPortWWN*   
用于回调的全球名称（WWN）。 端口\_标识符，它具有使用物理光纤通道端口发现的 SMP 端口\_标识符的最小值。 如果未使用物理光纤通道端口发现任何 SMP 端口，则它的值为零。

*标志*   
指示 HBA 及其微型端口驱动程序提供与永久性绑定相关的一组特定功能的位图。 有关此参数可以具有的值的列表，请参阅\_类型 WMI 类限定符\_绑定 HBA 的说明。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SetBindingSupport\_OUT 结构的 HBAStatus 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS\_SM\_TargetInformationMethods WMI 类。

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_SetBindingSupport\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setbindingsupport_in)

[**SM\_SetBindingSupport\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setbindingsupport_out)

 

 







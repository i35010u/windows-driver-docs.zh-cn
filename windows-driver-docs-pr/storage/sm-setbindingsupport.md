---
title: SM \_ SetBindingSupport 函数
description: SM \_ SetBindingSupport 方法设置所指示的端口的绑定功能。
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
ms.openlocfilehash: a25b667734d32c19bcd18dd2d94219be29ae59ad
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191641"
---
# <a name="sm_setbindingsupport-function"></a>SM \_ SetBindingSupport 函数


SM \_ SetBindingSupport 方法设置所指示的端口的绑定功能。

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
将检索其持久性绑定的端口的全球名称 (WWN) 。

*DomainPortWWN*   
用于回调的全球名称 (WWN) 。 它是端口 \_ 标识符，它具有 \_ 使用物理光纤通道端口发现的 SMP 端口的任意端口标识符的最小值。 如果未使用物理光纤通道端口发现任何 SMP 端口，则它的值为零。

*随意*   
指示 HBA 及其微型端口驱动程序提供与永久性绑定相关的一组特定功能的位图。 有关此参数可以具有的值的列表，请参阅 HBA \_ 绑定 \_ 类型 WMI 类限定符的说明。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SetBindingSupport OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS \_ SM \_ TargetInformationMethods WMI 类。

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
<td align="left">“桌面”</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**SM \_ SetBindingSupport \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setbindingsupport_in)

[**SM \_ SetBindingSupport \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setbindingsupport_out)

 


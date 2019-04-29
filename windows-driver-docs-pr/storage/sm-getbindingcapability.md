---
title: SM\_GetBindingCapability 函数
description: SM\_GetBindingCapability 方法检索所指示的端口的绑定功能。
ms.assetid: 11b7df8b-2694-4c49-a97a-ed475f3e841f
keywords:
- SM_GetBindingCapability 函数存储设备
topic_type:
- apiref
api_name:
- SM_GetBindingCapability
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 89cf5cd97caac3b8eef64b46e0b919dc0c13c5cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356703"
---
# <a name="smgetbindingcapability-function"></a>SM\_GetBindingCapability 函数


SM\_GetBindingCapability 方法检索所指示的端口的绑定功能。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_GetBindingCapability(
   [in, HBAType("HBA_WWN")] uint8                 HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                 DomainPortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS        HBAStatus,
   [out, HBAType("SMHBA_BIND_CAPABILITY")] uint32 HBAType
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
将检索其永久绑定的端口全球通用名称 (WWN)。

*DomainPortWWN*   
全球通用名称 (WWN) 的回调。 是的端口\_具有任何端口的最小值的标识符\_已使用发现的物理光纤通道端口的 SMP 端口的标识符。 如果没有 SMP 端口已发现通过使用物理光纤通道端口，它具有值为零。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)结构。 微型端口驱动程序 GetBindingCapability 在 HBAStatus 成员中返回此信息\_结构。

*HBAType*   
若要提供一组特定的功能与永久绑定相关的 HBA 和其微型端口驱动程序的功能。 此参数可以具有的值的列表，请参阅 HBA 的说明\_绑定\_类型 WMI 类限定符。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

SM\_GetBindingSupport 方法返回当前已启用的绑定功能，而 SM\_GetBindingCapability 方法指示而无需引用是否端口的绑定功能特定的绑定或未启用。 此 WMI 方法属于 MS\_SM\_TargetInformationMethods WMI 类。

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
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_GetBindingCapability\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566224)

[**SM\_GetBindingCapability\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566227)

 

 







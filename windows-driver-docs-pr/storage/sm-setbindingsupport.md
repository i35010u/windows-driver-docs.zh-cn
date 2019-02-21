---
title: SM\_SetBindingSupport 函数
description: SM\_SetBindingSupport 方法设置为指定的端口的绑定功能。
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
ms.openlocfilehash: c022ee410efb7d7e97fe9be62eeff5a6a535842d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544304"
---
# <a name="smsetbindingsupport-function"></a>SM\_SetBindingSupport 函数


SM\_SetBindingSupport 方法设置为指定的端口的绑定功能。

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
将检索其永久绑定的端口全球通用名称 (WWN)。

*DomainPortWWN*   
全球通用名称 (WWN) 的回调。 是的端口\_具有任何端口的最小值的标识符\_发现通过使用物理光纤通道端口的 SMP 端口的标识符。 如果没有 SMP 端口已发现通过使用物理光纤通道端口，它具有值为零。

*标志*   
指示 HBA 的功能和其微型端口驱动程序提供一组特定的功能与永久绑定相关的位图。 此参数可以具有的值的列表，请参阅 HBA 的说明\_绑定\_类型 WMI 类限定符。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序 SetBindingSupport 在 HBAStatus 成员中返回此信息\_结构。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_SetBindingSupport\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566330)

[**SM\_SetBindingSupport\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566331)

 

 







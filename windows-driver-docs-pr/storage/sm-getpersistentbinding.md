---
title: SM\_GetPersistentBinding 函数
description: SM\_GetPersistentBinding 方法检索 HBA 微型端口驱动程序使用的绑定。 这些绑定的逻辑单元将特定于操作系统的 LUN 信息映射到光纤通道协议 (FCP) 标识符。
ms.assetid: 74a67e91-c3b3-462a-8810-a9eae64e02a7
keywords:
- SM_GetPersistentBinding 函数存储设备
topic_type:
- apiref
api_name:
- SM_GetPersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2e1e83efd3f45efcae3d3185f210cb60635ead03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351667"
---
# <a name="smgetpersistentbinding-function"></a>SM\_GetPersistentBinding 函数


SM\_GetPersistentBinding 方法检索 HBA 微型端口驱动程序使用的绑定。 这些绑定的逻辑单元将特定于操作系统的 LUN 信息映射到光纤通道协议 (FCP) 标识符。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_GetPersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                          DomainPortWWN[8],
   [in] uint32                                             InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                 HBAStatus,
   [out] uint32                                            TotalEntryCount,
   [out] uint32                                            OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] MS_SMHBA_BINDINGENTRY Bindings[]
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
将检索其永久绑定的端口全球通用名称 (WWN)。

*DomainPortWWN*   
全球通用名称 (WWN) 的回调。 是的端口\_具有任何端口的最小值的标识符\_已使用发现的物理光纤通道端口的 SMP 端口的标识符。 如果没有 SMP 端口已发现通过使用物理光纤通道端口，它具有值为零。

*InEntryCount*   
WMI 提供程序可以报告条目参数中的绑定条目数。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)结构。 微型端口驱动程序 GetPersistentBinding 在 HBAStatus 成员中返回此信息\_结构。

*TotalEntryCount*   
HBA 与相关联的永久绑定的总数。

*OutEntryCount*   
SM 检索的永久绑定的总数\_GetPersistentBinding 方法。 此值将为小于或等于 TotalEntryCount。

*绑定*   
类型 MS 的结构数组\_SMHBA\_BINDINGENTRY 描述 HBA 的绑定之间的操作系统和光纤通道协议 (FCP) 标识符。

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
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_GetPersistentBinding\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566246)

[**SM\_GetPersistentBinding\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566248)

 

 







---
title: SM\_SetPersistentBinding 函数
description: SM\_SetPersistentBinding 方法设置 HBA 微型端口驱动程序用于将特定于操作系统的 LUN 信息映射到光纤通道协议 (FCP) 标识符，对于逻辑单元的绑定。
ms.assetid: 722f7216-9ff4-4f12-a4fe-e1f8f9e594e1
keywords:
- SM_SetPersistentBinding 函数存储设备
topic_type:
- apiref
api_name:
- SM_SetPersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e6fa74b90d0e3dbbf720487ef3f8b57dcd2ac383
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364053"
---
# <a name="smsetpersistentbinding-function"></a>SM\_SetPersistentBinding 函数


SM\_SetPersistentBinding 方法设置 HBA 微型端口驱动程序用于将特定于操作系统的 LUN 信息映射到光纤通道协议 (FCP) 标识符，对于逻辑单元的绑定。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SetPersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                        HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                        DomainPortWWN[8],
   [in] uint32                                           InEntryCount,
   [in, WmiSizeIs("InEntryCount")] MS_SMHBA_BINDINGENTRY Entry[],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS               HBAStatus,
   [out] uint32                                          OutStatusCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS               EntryStatus
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
将设置其持久性的绑定的端口全球通用名称 (WWN)。

*DomainPortWWN*   
全球通用名称 (WWN) 的回调。 是的端口\_具有任何端口的最小值的标识符\_使用发现的物理光纤通道端口的 SMP 端口的标识符。 如果没有 SMP 端口已发现通过使用物理光纤通道端口，它具有值为零。

*InEntryCount*   
WMI 提供程序可以报告条目参数中的绑定条目数。

*条目*   
类型 SMHBA 的结构数组\_SCSIENTRY 描述之间的操作系统和 SAS 标识符的 HBA 的绑定。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序 GetPersistentBinding 在 HBAStatus 成员中返回此信息\_结构。

*OutStatusCount*   
SM 检索的永久绑定的总数\_GetPersistentBinding 方法。 此值将为小于或等于 TotalEntryCount。

*EntryStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序 GetPersistentBinding 在 HBAStatus 成员中返回此信息\_结构。

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

[**SM\_SetPersistentBinding\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566334)

[**SM\_SetPersistentBinding\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566335)

 

 







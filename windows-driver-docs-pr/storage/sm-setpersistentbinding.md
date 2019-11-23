---
title: SM\_SetPersistentBinding 函数
description: SM\_SetPersistentBinding 方法将 HBA 微型端口驱动程序使用的绑定设置为逻辑单元将特定于 OS 的 LUN 信息映射到光纤通道协议（FCP）标识符。
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
ms.openlocfilehash: f56405988affefbc05a1bee820130cd67414fca7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845448"
---
# <a name="sm_setpersistentbinding-function"></a>SM\_SetPersistentBinding 函数


SM\_SetPersistentBinding 方法将 HBA 微型端口驱动程序使用的绑定设置为逻辑单元将特定于 OS 的 LUN 信息映射到光纤通道协议（FCP）标识符。

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

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
将设置其持久性绑定的端口的全球名称（WWN）。

*DomainPortWWN*   
用于回调的全球名称（WWN）。 端口\_标识符，它具有使用物理光纤通道端口发现的 SMP 端口\_标识符的最小值。 如果未使用物理光纤通道端口发现任何 SMP 端口，则它的值为零。

*InEntryCount*   
WMI 提供程序可在 Entry 参数中报告的绑定项的数目。

*条目*   
类型为 SMHBA\_SCSIENTRY 的结构的数组，它描述了操作系统与 SAS 标识符之间的 HBA 绑定。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 GetPersistentBinding\_OUT 结构的 HBAStatus 成员中返回此信息。

*OutStatusCount*   
SM\_GetPersistentBinding 方法检索的永久绑定的总数。 此值将小于或等于 TotalEntryCount。

*EntryStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 GetPersistentBinding\_OUT 结构的 HBAStatus 成员中返回此信息。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_SetPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setpersistentbinding_in)

[**SM\_SetPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setpersistentbinding_out)

 

 







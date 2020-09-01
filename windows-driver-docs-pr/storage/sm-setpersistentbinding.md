---
title: SM \_ SetPersistentBinding 函数
description: SM \_ SetPersistentBinding 方法将 HBA 微型端口驱动程序所使用的绑定设置为将特定于 OS 的 LUN 信息映射到光纤通道协议， (FCP) 逻辑单元标识符。
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
ms.openlocfilehash: 5ca18a3f3b702c28061db089cffc4542e3efd906
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192645"
---
# <a name="sm_setpersistentbinding-function"></a>SM \_ SetPersistentBinding 函数


SM \_ SetPersistentBinding 方法将 HBA 微型端口驱动程序所使用的绑定设置为将特定于 OS 的 LUN 信息映射到光纤通道协议， (FCP) 逻辑单元标识符。

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
将设置其持久性绑定的端口的全球名称 (WWN) 。

*DomainPortWWN*   
用于回调的全球名称 (WWN) 。 它是端口 \_ 标识符，它具有 \_ 使用物理光纤通道端口发现的 SMP 端口的任意端口标识符的最小值。 如果未使用物理光纤通道端口发现任何 SMP 端口，则它的值为零。

*InEntryCount*   
WMI 提供程序可在 Entry 参数中报告的绑定项的数目。

*条目*   
SMHBA SCSIENTRY 类型的结构的数组 \_ ，它描述了操作系统与 SAS 标识符之间的 HBA 绑定。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 GetPersistentBinding OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

*OutStatusCount*   
SM GetPersistentBinding 方法检索的永久绑定的总数 \_ 。 此值将小于或等于 TotalEntryCount。

*EntryStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 GetPersistentBinding OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>注解
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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**SM \_ SetPersistentBinding \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setpersistentbinding_in)

[**SM \_ SetPersistentBinding \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setpersistentbinding_out)

 


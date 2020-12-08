---
title: SM \_ GetPersistentBinding 函数
description: SM \_ GetPersistentBinding 方法检索 HBA 微型端口驱动程序使用的绑定。 这些绑定将特定于 OS 的 LUN 信息映射到光纤通道协议， (FCP) 逻辑单元标识符。
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
ms.openlocfilehash: 0781fb32d64b5d84cef6c97713fd0229aa923d38
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788233"
---
# <a name="sm_getpersistentbinding-function"></a>SM \_ GetPersistentBinding 函数


SM \_ GetPersistentBinding 方法检索 HBA 微型端口驱动程序使用的绑定。 这些绑定将特定于 OS 的 LUN 信息映射到光纤通道协议， (FCP) 逻辑单元标识符。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_GetPersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                          DomainPortWWN[8],
   [in] uint32                                             InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                 HBAStatus,
   [out] uint32                                            TotalEntryCount,
   [out] uint32                                            OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] MS_SMHBA_BINDINGENTRY Bindings[]
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
将检索其持久性绑定的端口的全球名称 (WWN) 。

*DomainPortWWN*   
用于回调的全球名称 (WWN) 。 它是端口 \_ 标识符，它具有 \_ 使用物理光纤通道端口发现的 SMP 端口的任意端口标识符的最小值。 如果未使用物理光纤通道端口发现任何 SMP 端口，则它的值为零。

*InEntryCount*   
WMI 提供程序可在 Entry 参数中报告的绑定项的数目。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md) 结构。 微型端口驱动程序在 GetPersistentBinding OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

*TotalEntryCount*   
与 HBA 关联的永久绑定的总数。

*OutEntryCount*   
SM GetPersistentBinding 方法检索的永久绑定的总数 \_ 。 此值将小于或等于 TotalEntryCount。

*绑定*   
类型为 MS SMHBA BINDINGENTRY 的结构的数组 \_ \_ ，它描述了操作系统与光纤通道协议之间的 HBA 绑定 (FCP) 标识符。

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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**SM \_ GetPersistentBinding \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getpersistentbinding_in)

[**SM \_ GetPersistentBinding \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getpersistentbinding_out)

 


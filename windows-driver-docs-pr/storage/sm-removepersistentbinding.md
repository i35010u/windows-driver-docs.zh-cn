---
title: SM\_RemovePersistentBinding 函数
description: SM\_RemovePersistentBinding 方法删除指定适配器端口的指定 SCSI Id 的一个或多个永久性绑定。
ms.assetid: 475c2f5f-4a1c-48b4-9a43-81d03b1b737d
keywords:
- SM_RemovePersistentBinding 函数存储设备
topic_type:
- apiref
api_name:
- SM_RemovePersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0bc577d50fd214358cb10addfb44e799f1de7cdd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845476"
---
# <a name="sm_removepersistentbinding-function"></a>SM\_RemovePersistentBinding 函数


SM\_RemovePersistentBinding 方法删除指定适配器端口的指定 SCSI Id 的一个或多个永久性绑定。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_RemovePersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                      HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                      DomainPortWWN[8],
   [in] uint32                                         EntryCount,
   [in, WmiSizeIs("EntryCount")] MS_SMHBA_BINDINGENTRY Entry[],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS             HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
将删除其持久性绑定的端口的全球名称（WWN）。

*DomainPortWWN*   
用于回调的全球名称（WWN）。 端口\_标识符，它具有使用物理光纤通道端口发现的任何端口\_标识符的最小值。 如果未使用物理光纤通道端口发现任何 SMP 端口，则它的值为零。

*EntryCount*   
WMI 提供程序可在 Entry 参数中报告的绑定项的数目。

*条目*   
用于永久性绑定的 MS\_SMHBA\_BINDINGENTRY 类型的列表。

*HBAStatus*   
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

[**SM\_RemovePersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removepersistentbinding_in)

[**SM\_RemovePersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removepersistentbinding_out)

 

 







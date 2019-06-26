---
title: SM\_RemovePersistentBinding 函数
description: SM\_RemovePersistentBinding 方法中删除一个或多个永久性绑定到指定的 SCSI Id 指定的适配器的端口。
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
ms.openlocfilehash: f70791b579d69e2182d89fce6b3eab363fe84f8a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384300"
---
# <a name="smremovepersistentbinding-function"></a>SM\_RemovePersistentBinding 函数


SM\_RemovePersistentBinding 方法中删除一个或多个永久性绑定到指定的 SCSI Id 指定的适配器的端口。

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

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
将删除其持久性的绑定的端口全球通用名称 (WWN)。

*DomainPortWWN*   
全球通用名称 (WWN) 的回调。 是的端口\_具有任何端口的最小值的标识符\_已使用发现的物理光纤通道端口的 SMP 端口的标识符。 如果没有 SMP 端口已发现通过使用物理光纤通道端口，它具有值为零。

*EntryCount*   
WMI 提供程序可以报告条目参数中的绑定条目数。

*条目*   
一系列 MS\_SMHBA\_BINDINGENTRY 绑定类型为永久。

*HBAStatus*   
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

[**SM\_RemovePersistentBinding\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_removepersistentbinding_in)

[**SM\_RemovePersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_removepersistentbinding_out)

 

 







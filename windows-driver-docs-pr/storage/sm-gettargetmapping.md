---
title: SM\_GetTargetMapping 函数
description: SM\_GetTargetMapping WMI 方法检索这些逻辑单元的唯一标识一系列的操作系统的逻辑单元的信息和光纤通道协议 (FCP) 标识符之间的映射。
ms.assetid: db18920c-327d-4349-8821-6d7fb68eccbd
keywords:
- SM_GetTargetMapping 函数存储设备
topic_type:
- apiref
api_name:
- SM_GetTargetMapping
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d105b8218755279ceb7f442ff63f96c57c7127de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351662"
---
# <a name="smgettargetmapping-function"></a>SM\_GetTargetMapping 函数


SM\_GetTargetMapping WMI 方法检索这些逻辑单元的唯一标识一系列的操作系统的逻辑单元的信息和光纤通道协议 (FCP) 标识符之间的映射。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_GetTargetMapping(
   [in, HBAType("HBA_WWN")] uint8                       HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                       DomainPortWWN[8],
   [in] uint32                                          InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS              HBAStatus,
   [out] uint32                                         TotalEntryCount,
   [out] uint32                                         OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] MS_SMHBA_SCSIENTRY Entry[]
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
要检索其表映射的端口全球通用名称 (WWN)。 此信息传递到 GetTargetMapping HbaPortWWN 成员中的微型端口驱动程序\_结构中。

*DomainPortWWN*   
全球通用名称 (WWN) 的回调。 是的端口\_与任何端口的最小值的标识符\_使用发现的物理光纤通道端口的 SMP 端口的标识符。 如果没有 SMP 端口已发现通过使用物理光纤通道端口，它具有值为零。

*InEntryCount*   
WMI 提供程序可以报告条目参数中的绑定条目数。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)结构。 微型端口驱动程序 GetFcpTargetMapping 在 HBAStatus 成员中返回此信息\_结构。

*TotalEntryCount*   
HBA 与相关联的永久绑定的总数。

*OutEntryCount*   
SM 检索的映射的总数量\_GetTargetMapping 方法。 此值将为小于或等于 TotalEntryCount。

*条目*   
类型 MS 的结构数组\_SMHBA\_SCSIENTRY 描述 HBA 的绑定之间的操作系统和光纤通道协议 (FCP) 标识符。

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

[**SM\_GetTargetMapping\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566256)

[**SM\_GetTargetMapping\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566258)

 

 







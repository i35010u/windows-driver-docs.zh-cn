---
title: SM\_RemoveTarget 函数
description: SM\_RemoveTarget WMI 方法配置 WMI 提供程序，以便它将停止将传递到 WMI 客户端所指示的目标与相关联的事件。
ms.assetid: 9be2a40c-299a-4d92-b9a2-ef60eb6d90e9
keywords:
- SM_RemoveTarget 函数存储设备
topic_type:
- apiref
api_name:
- SM_RemoveTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a334e101af21fe94a3a2d5adc58fd5d1791c9cd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561902"
---
# <a name="smremovetarget-function"></a>SM\_RemoveTarget 函数


SM\_RemoveTarget WMI 方法配置 WMI 提供程序，以便它将停止将传递到 WMI 客户端所指示的目标与相关联的事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_RemoveTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
唯一标识应从其事件报告给 WMI 客户端的端口的列表中删除的本地端口 64-bit 全球通用名称 (WWN)。 有关全球范围内的名称的详细信息，请参阅 T11 委员会*光纤通道 HBA API*规范。

*DiscoveredPortWWN*   
全球通用名称 (WWN)，该值指示应从其事件报告给 WMI 客户端的端口的列表中删除的远程发现的端口。

*AllTargets*   
要停止报告的事件。 如果此成员为零，则 WMI 提供程序客户端停止报告与由 DiscoveredPortWWN 的端口相关联的事件。 如果此成员为非零值，则会停止 WMI 提供程序报告的所有事件相关都联的任何目标。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_RemoveTarget\_结构。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS\_SM\_将 EventControl WMI 类。

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

[**SM\_RemoveTarget\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566280)

[**SM\_RemoveTarget\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566283)

 

 







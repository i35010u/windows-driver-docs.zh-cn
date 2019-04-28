---
title: RemoveTarget 函数
description: RemoveTarget WMI 方法配置 WMI 提供程序，以便它将停止将传递到 WMI 客户端所指示的目标与关联的事件。
ms.assetid: 413cee3c-5e3a-4012-925b-b4699fbd2e1b
keywords:
- RemoveTarget 函数存储设备
topic_type:
- apiref
api_name:
- RemoveTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a1faffa08cb47dba596f0e6cb1fbdb34b2381689
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349145"
---
# <a name="removetarget-function"></a>RemoveTarget 函数


**RemoveTarget** WMI 方法配置 WMI 提供程序，以便它将停止将传递到 WMI 客户端所指示的目标与关联的事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemoveTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
唯一标识应从其事件报告给 WMI 客户端的端口的列表中删除的本地端口 64 位全球通用名称 (WWN)。 全球通用名称的讨论，请参阅 T11 委员会*光纤通道 HBA API*规范。

*DiscoveredPortWWN*   
指示应从其事件报告给 WMI 客户端的端口的列表中删除的远程发现的端口的 WWN。

*AllTargets*   
要停止报告的事件。 如果此成员为零，WMI 提供程序客户端将停止报告事件与端口所指示的关联*DiscoveredPortWWN*。 如果此成员为非零值，则 WMI 提供程序将停止报告的所有事件相关都联的任何目标。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **RemoveTarget\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564039)结构。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_将 EventControl WMI 类](msfc-eventcontrol-wmi-class.md)。

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
<td align="left">Hbapiwmi.h （包括 Hbapiwmi.h、 Hbaapi.h 或 Hbaapi.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**RemoveTarget\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff564033)

[**RemoveTarget\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff564039)

 

 







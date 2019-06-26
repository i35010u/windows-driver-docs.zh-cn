---
title: AddTarget 函数
description: AddTarget WMI 方法配置 WMI 提供程序，以通知有关与所指示的目标相关联的事件的 WMI 客户端。
ms.assetid: 9aac339b-a9b4-4de7-99dd-fa5f8889a686
keywords:
- AddTarget 函数存储设备
topic_type:
- apiref
api_name:
- AddTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 74d39de161128efbbb40607063bc0d3a085e72e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362683"
---
# <a name="addtarget-function"></a>AddTarget 函数


**AddTarget** WMI 方法配置 WMI 提供程序，以通知有关与所指示的目标相关联的事件的 WMI 客户端。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void AddTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN\[8\]*    
全球范围内的本地端口 WMI 客户端将接收其事件的名称。

*DiscoveredPortWWN\[8\]*    
指定 WMI 客户端将接收其事件的已发现的目标全球通用名称。

*AllTargets*   
目标事件到报表的作用域。 如果此成员为零，WMI 客户端将接收与端口所指示的关联的事件*DiscoveredPortWWN*。 如果此成员为非零值，WMI 客户端将接收与所有当前已发现的目标以及将来发现的目标相关联的所有事件。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **AddTarget\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_addtarget_out)结构。

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


[**AddTarget\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_addtarget_in)

[**AddTarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_addtarget_out)

 

 







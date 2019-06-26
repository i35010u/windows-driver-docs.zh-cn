---
title: SM\_AddTarget 函数
description: SM\_AddTarget WMI 方法配置 WMI 提供程序，以通知有关与所指示的目标相关联的事件的 WMI 客户端。
ms.assetid: 78e19496-1eb0-4d05-8637-f2e6d123208b
keywords:
- SM_AddTarget 函数存储设备
topic_type:
- apiref
api_name:
- SM_AddTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c9a6e693b3b4cdabb27426c1b2453d3f382af595
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384320"
---
# <a name="smaddtarget-function"></a>SM\_AddTarget 函数


SM\_AddTarget WMI 方法配置 WMI 提供程序，以通知有关与所指示的目标相关联的事件的 WMI 客户端。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_AddTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DomainPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
全球通用名称 (WWN) 的本地端口 WMI 客户端将接收其事件。

*DiscoveredPortWWN*   
WMI 客户端将收到指定其事件的发现的目标全球通用名称 (WWN)。

*DomainPortWWN*   
全球通用名称 (WWN)，指定本地端口 WMI 客户端将接收其事件的 SAS 域全球通用名称。

*AllTargets*   
目标事件到报表的作用域。 如果此成员为零，WMI 客户端将接收与所指示的 DiscoveredPortWWN 的端口相关联的事件。 如果此成员为非零值，WMI 客户端将接收与所有当前已发现的目标以及将来发现的目标相关联的所有事件。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_AddTarget\_结构。

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

[**SM\_AddTarget\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_addtarget_in)

[**SM\_AddTarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_addtarget_out)

 

 







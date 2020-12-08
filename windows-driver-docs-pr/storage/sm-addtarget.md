---
title: SM \_ AddTarget 函数
description: SM \_ ADDTARGET wmi 方法将 wmi 提供程序配置为通知 wmi 客户端与所指示的目标相关联的事件。
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
ms.openlocfilehash: 94ac2d27753853305d90e4c88f6c981d289ac12b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839373"
---
# <a name="sm_addtarget-function"></a>SM \_ AddTarget 函数


SM \_ ADDTARGET wmi 方法将 wmi 提供程序配置为通知 wmi 客户端与所指示的目标相关联的事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_AddTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DomainPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
 (的全球名称，它是 WMI 客户端将接收其事件的本地端口的 WWN) 。

*DiscoveredPortWWN*   
全球名称 (WWN) 指定 WMI 客户端将接收其事件的发现目标。

*DomainPortWWN*   
全球名称 (WWN) 指定 WMI 客户端将接收其事件的本地端口的全球 SAS 域名称。

*AllTargets*   
要报告的目标事件的范围。 如果此成员为零，则 WMI 客户端将接收与 DiscoveredPortWWN 指示的端口关联的事件。 如果此成员为非零，则 WMI 客户端将接收与所有当前发现的目标以及将来发现的目标关联的所有事件。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SM \_ AddTarget OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS \_ SM \_ EventControl WMI 类。

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

[**SM \_ AddTarget \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addtarget_in)

[**SM \_ AddTarget \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addtarget_out)

 


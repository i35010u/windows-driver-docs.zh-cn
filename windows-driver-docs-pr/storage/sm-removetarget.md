---
title: SM \_ RemoveTarget 函数
description: SM \_ REMOVETARGET wmi 方法配置 wmi 提供程序，使其停止将与指示的目标关联的事件传递给 WMI 客户端。
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
ms.openlocfilehash: a5ea021e624263de648e2b21d914215f0fd1f2b6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186389"
---
# <a name="sm_removetarget-function"></a>SM \_ RemoveTarget 函数


SM \_ REMOVETARGET wmi 方法配置 wmi 提供程序，使其停止将与指示的目标关联的事件传递给 WMI 客户端。

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

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
64位全球名称 (WWN) ，用于唯一标识应该从其事件报告给 WMI 客户端的端口列表中删除的本地端口。 有关全球名称的详细信息，请参阅 T11 委员会 *光纤通道 HBA API* 规范。

*DiscoveredPortWWN*   
全球名称 (WWN) ，它指示远程发现的端口，应从其事件报告给 WMI 客户端的端口列表中删除该端口。

*AllTargets*   
要停止报告的事件。 如果此成员为零，则 WMI 提供程序客户端将停止报告与 DiscoveredPortWWN 指示的端口关联的事件。 如果此成员为非零，则 WMI 提供程序将停止报告所有关联的事件。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SM \_ RemoveTarget OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

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
<td align="left">“桌面”</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**SM \_ RemoveTarget \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removetarget_in)

[**SM \_ RemoveTarget \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removetarget_out)

 


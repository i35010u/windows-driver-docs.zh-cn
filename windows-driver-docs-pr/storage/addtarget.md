---
title: AddTarget 函数
description: AddTarget WMI 方法将 WMI 提供程序配置为通知 WMI 客户端与所指示的目标相关联的事件。
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
ms.openlocfilehash: 696a6299f6bfeec7a58332d6465e749fa587935d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188029"
---
# <a name="addtarget-function"></a>AddTarget 函数


**AddTarget** wmi 方法将 wmi 提供程序配置为通知 wmi 客户端与所指示的目标相关联的事件。

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

<a name="parameters"></a>参数
----------

*HbaPortWWN \[ 8\]*   
WMI 客户端将接收其事件的本地端口的全球名称。

*DiscoveredPortWWN \[ 8\]*   
一个全球名称，指定 WMI 客户端将接收其事件的发现目标。

*AllTargets*   
要报告的目标事件的范围。 如果此成员为零，则 WMI 客户端将接收与 *DiscoveredPortWWN*指示的端口关联的事件。 如果此成员为非零，则 WMI 客户端将接收与所有当前发现的目标以及将来发现的目标关联的所有事件。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**AddTarget \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addtarget_out)结构的**HBAStatus**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>注解
-------

此 WMI 方法属于 [MSFC \_ EventControl WMI 类](msfc-eventcontrol-wmi-class.md)。

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
<td align="left"><p>Header</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**AddTarget \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addtarget_in)

[**AddTarget \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addtarget_out)

 


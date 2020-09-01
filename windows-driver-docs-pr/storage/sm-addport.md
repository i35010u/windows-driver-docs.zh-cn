---
title: SM \_ AddPort 函数
description: SM \_ ADDPORT wmi 方法将 wmi 提供程序配置为通知 wmi 客户端与所指示的端口关联的事件。
ms.assetid: 1667487e-80b1-47eb-9f3c-2f5e1909c73b
keywords:
- SM_AddPort 函数存储设备
topic_type:
- apiref
api_name:
- SM_AddPort
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1329bc028a6a050496ead1695e5b606f4f86de2d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188488"
---
# <a name="sm_addport-function"></a>SM \_ AddPort 函数


SM \_ ADDPORT wmi 方法将 wmi 提供程序配置为通知 wmi 客户端与所指示的端口关联的事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_AddPort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [in, EVENT_TYPES_QUALIFIERS] uint32     EventType,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*PortWWN*   
全球名称 (WWN) ，用于指示要报告其事件的端口。

*EventType*   
事件的类型。 可分配给此成员的值由事件 \_ 类型 \_ 限定符 WMI 类限定符定义。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SM \_ AddPort OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

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

[**SM \_ AddPort \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addport_in)

[**SM \_ AddPort \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addport_out)

 


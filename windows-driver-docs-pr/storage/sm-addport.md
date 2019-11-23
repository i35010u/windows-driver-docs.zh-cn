---
title: SM\_AddPort 函数
description: SM\_AddPort WMI 方法将 WMI 提供程序配置为通知 WMI 客户端与所指示的端口关联的事件。
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
ms.openlocfilehash: fb25c4d9a97825af5e9d2bbd60e34cb7f5e852c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845492"
---
# <a name="sm_addport-function"></a>SM\_AddPort 函数


SM\_AddPort WMI 方法将 WMI 提供程序配置为通知 WMI 客户端与所指示的端口关联的事件。

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
一个全球通用名称（WWN），指示要报告其事件的端口。

*事件*=   
事件的类型。 可分配给此成员的值由事件\_类型\_限定符 WMI 类限定符定义。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SM\_AddPort\_OUT 结构的 HBAStatus 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS\_SM\_EventControl WMI 类。

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
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_AddPort\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addport_in)

[**SM\_AddPort\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addport_out)

 

 







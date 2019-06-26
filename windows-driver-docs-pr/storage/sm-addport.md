---
title: SM\_端口函数
description: SM\_端口 WMI 方法配置 WMI 提供程序，以通知有关与指定的端口相关联的事件的 WMI 客户端。
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
ms.openlocfilehash: 613500602248a57175b992ee22287bbccf447a37
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384321"
---
# <a name="smaddport-function"></a>SM\_端口函数


SM\_端口 WMI 方法配置 WMI 提供程序，以通知有关与指定的端口相关联的事件的 WMI 客户端。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_AddPort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [in, EVENT_TYPES_QUALIFIERS] uint32     EventType,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*PortWWN*   
全球通用名称 (WWN)，指示其事件将被报告的端口。

*EventType*   
该事件的类型。 可以分配给此成员的值定义事件\_类型\_限定符 WMI 类限定符。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_端口\_结构。

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

[**SM\_AddPort\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_addport_in)

[**SM\_AddPort\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_addport_out)

 

 







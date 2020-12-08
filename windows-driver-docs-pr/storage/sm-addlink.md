---
title: SM \_ AddLink 函数
description: SM \_ ADDLINK wmi 方法将 wmi 提供程序配置为通知 wmi 客户端 fabric 链接事件。
keywords:
- SM_AddLink 函数存储设备
topic_type:
- apiref
api_name:
- SM_AddLink
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4c2035d3105a2eee14a21b70cff4987dd293ba9e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830943"
---
# <a name="sm_addlink-function"></a>SM \_ AddLink 函数


SM \_ ADDLINK wmi 方法将 wmi 提供程序配置为通知 wmi 客户端 fabric 链接事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_AddLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SM \_ AddLink OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

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

[**SM \_ AddLink \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addlink_out)

 


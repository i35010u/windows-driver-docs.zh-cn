---
title: AddLink 函数
description: AddLink WMI 方法将 WMI 提供程序配置为通知 WMI 客户端 fabric 链接事件。
keywords:
- AddLink 函数存储设备
topic_type:
- apiref
api_name:
- AddLink
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aca37109bd248a47d05cdea0db213501848f315f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804789"
---
# <a name="addlink-function"></a>AddLink 函数


**AddLink** wmi 方法将 wmi 提供程序配置为通知 wmi 客户端 fabric 链接事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void AddLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**AddLink \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addlink_out)结构的 **HBAStatus** 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
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
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi (包含 Hbaapi 或 Hbapiwmi) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**AddLink \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addlink_out)

 


---
title: SM \_ RemoveLink 函数
description: SM \_ REMOVELINK wmi 方法配置 wmi 提供程序，使其停止向 WMI 客户端传递 fabric 链接事件信息。
ms.assetid: 25f6b807-f921-44b6-b087-e5c6ec8c72ec
keywords:
- SM_RemoveLink 函数存储设备
topic_type:
- apiref
api_name:
- SM_RemoveLink
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4ca7477ffdcb88a17492b280e92b2ad4eb2957c2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186405"
---
# <a name="sm_removelink-function"></a>SM \_ RemoveLink 函数


SM \_ REMOVELINK wmi 方法配置 wmi 提供程序，使其停止向 WMI 客户端传递 fabric 链接事件信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_RemoveLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SM \_ RemoveLink OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

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

[**SM \_ RemoveLink \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removelink_out)

 


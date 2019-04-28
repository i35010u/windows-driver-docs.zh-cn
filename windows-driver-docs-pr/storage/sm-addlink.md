---
title: SM\_AddLink 函数
description: SM\_AddLink WMI 方法可配置要通知的 fabric 链接事件的 WMI 客户端的 WMI 提供程序。
ms.assetid: 29ddfdb7-232a-4715-bf36-5f64554ee608
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
ms.openlocfilehash: 7d2c4425fc238b3303634ce392ff040001b10e93
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341197"
---
# <a name="smaddlink-function"></a>SM\_AddLink 函数


SM\_AddLink WMI 方法可配置要通知的 fabric 链接事件的 WMI 客户端的 WMI 提供程序。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_AddLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_AddLink\_结构。

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

[**SM\_AddLink\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566210)

 

 







---
title: AddLink 函数
description: AddLink WMI 方法可配置要通知的 fabric 链接事件的 WMI 客户端的 WMI 提供程序。
ms.assetid: 67c17627-3f41-429b-a0f7-ec7782f1b1f9
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
ms.openlocfilehash: 02ebb17dd65988f398548f176bf367f9f21bbfb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542180"
---
# <a name="addlink-function"></a>AddLink 函数


**AddLink** WMI 方法可配置要通知的 fabric 链接事件的 WMI 客户端的 WMI 提供程序。

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
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **AddLink\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff550129)结构。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_将 EventControl WMI 类](msfc-eventcontrol-wmi-class.md)。

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
<td align="left">Hbapiwmi.h （包括 Hbaapi.h 或 Hbapiwmi.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**AddLink\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff550129)

 

 







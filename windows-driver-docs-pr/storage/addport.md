---
title: 端口函数
description: 端口 WMI 方法配置 WMI 提供程序，以通知有关与指定的端口相关联的事件的 WMI 客户端。
ms.assetid: d20021c8-2326-4fd8-b098-70ab8bf53ed3
keywords:
- 端口函数存储设备
topic_type:
- apiref
api_name:
- AddPort
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bfed85bd5efa233c728e5644757401062708e0f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547984"
---
# <a name="addport-function"></a>端口函数


**端口**WMI 方法配置 WMI 提供程序，以通知有关与指定的端口相关联的事件的 WMI 客户端。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void AddPort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*PortWWN\[8\]*   
全球通用名称，指示其事件将被报告的端口的说明。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[**端口\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff550132)结构。

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
<td align="left">Hbapiwmi.h （包括 Hbapiwmi.h、 Hbaapi.h 或 Hbaapi.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**AddPort\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff550131)

[**AddPort\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff550132)

 

 







---
title: RemoveLink 函数
description: RemoveLink WMI 方法配置 WMI 提供程序，以便它将停止将 fabric 链接事件信息传递给 WMI 客户端。
ms.assetid: 8c9f78ba-fdb8-4d6c-ab99-3492e0887572
keywords:
- RemoveLink 函数存储设备
topic_type:
- apiref
api_name:
- RemoveLink
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c237214b880e6a9d10dcfb5da8ffeb8c587ea9eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566994"
---
# <a name="removelink-function"></a>RemoveLink 函数


**RemoveLink** WMI 方法配置 WMI 提供程序，以便它将停止将 fabric 链接事件信息传递给 WMI 客户端。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemoveLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **RemoveLink\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff563987)结构。

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
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi.h （包括 Hbapiwmi.h、 Hbaapi.h 或 Hbaapi.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**RemoveLink\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff563987)

 

 







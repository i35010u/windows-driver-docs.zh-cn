---
title: RemovePort 函数
description: RemovePort WMI 方法配置 WMI 提供程序，以便它将停止将传递到 WMI 客户端的指定端口与关联的事件。
ms.assetid: 6e466a89-273b-4ed9-a0fe-5a8df745b28a
keywords:
- RemovePort 函数存储设备
topic_type:
- apiref
api_name:
- RemovePort
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ac9d2e8003a0eda0fc5788f26844d58d62c01e33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330046"
---
# <a name="removeport-function"></a>RemovePort 函数


**RemovePort** WMI 方法配置 WMI 提供程序，以便它将停止将传递到 WMI 客户端的指定端口与关联的事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemovePort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*PortWWN*   
指示应从其事件报告给 WMI 客户端的端口的列表中删除的端口的全球通用名称。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **RemovePort\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564017)结构。

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


[**RemovePort\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff564014)

[**RemovePort\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff564017)

 

 







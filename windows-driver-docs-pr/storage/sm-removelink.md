---
title: SM\_RemoveLink 函数
description: SM\_RemoveLink WMI 方法配置 WMI 提供程序，以便它将停止将 fabric 链接事件信息传递给 WMI 客户端。
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
ms.openlocfilehash: e8a12ed7cadcd80d0a588d96f14bc087a2d1bd85
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339065"
---
# <a name="smremovelink-function"></a>SM\_RemoveLink 函数


SM\_RemoveLink WMI 方法配置 WMI 提供程序，以便它将停止将 fabric 链接事件信息传递给 WMI 客户端。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_RemoveLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_RemoveLink\_结构。

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

[**SM\_RemoveLink\_出**](https://msdn.microsoft.com/library/windows/hardware/ff566265)

 

 







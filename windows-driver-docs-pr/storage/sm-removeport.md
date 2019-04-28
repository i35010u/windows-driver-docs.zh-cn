---
title: SM\_RemovePort 函数
description: SM\_RemovePort WMI 方法配置 WMI 提供程序，以便它将停止将传递到 WMI 客户端的指定端口与相关联的事件。
ms.assetid: aa868e5d-32d3-4bb0-9128-5f213bf62146
keywords:
- SM_RemovePort 函数存储设备
topic_type:
- apiref
api_name:
- SM_RemovePort
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 293191f9a9e3ede97d56c162dd977032bdd03653
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339047"
---
# <a name="smremoveport-function"></a>SM\_RemovePort 函数


SM\_RemovePort WMI 方法配置 WMI 提供程序，以便它将停止将传递到 WMI 客户端的指定端口与相关联的事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_RemovePort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [in, EVENT_TYPES_QUALIFIERS] uint32     EventType,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*PortWWN*   
全球通用名称 (WWN)，该值指示应从其事件报告给 WMI 客户端的端口的列表中删除的端口。

*EventType*   
该事件的类型。 可以分配给此成员的值定义事件\_类型\_限定符 WMI 类限定符。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_RemovePort\_结构。

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

[**SM\_RemovePort\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566274)

[**SM\_RemovePort\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566276)

 

 







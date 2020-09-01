---
title: RemovePort 函数
description: RemovePort WMI 方法配置 WMI 提供程序，使其停止将与所指示的端口关联的事件传递给 WMI 客户端。
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
ms.openlocfilehash: 20728630cde512e7bb2499ca886a9750c465a291
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191120"
---
# <a name="removeport-function"></a>RemovePort 函数


**RemovePort** wmi 方法配置 wmi 提供程序，使其停止将与所指示的端口关联的事件传递给 WMI 客户端。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemovePort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*PortWWN*   
一个全球名称，用于指示应从端口列表中删除的端口，这些端口的事件报告给 WMI 客户端。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**RemovePort \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removeport_out)结构的**HBAStatus**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>注解
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
<td align="left"><p>Header</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**RemovePort \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removeport_in)

[**RemovePort \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removeport_out)

 


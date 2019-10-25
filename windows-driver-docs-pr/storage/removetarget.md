---
title: RemoveTarget 函数
description: RemoveTarget WMI 方法配置 WMI 提供程序，使其停止将与指示的目标关联的事件传递给 WMI 客户端。
ms.assetid: 413cee3c-5e3a-4012-925b-b4699fbd2e1b
keywords:
- RemoveTarget 函数存储设备
topic_type:
- apiref
api_name:
- RemoveTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ebab0c1eaae0936aaff6b04db55726cfd5976eb0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842701"
---
# <a name="removetarget-function"></a>RemoveTarget 函数


**RemoveTarget** wmi 方法配置 wmi 提供程序，使其停止将与指示的目标关联的事件传递给 WMI 客户端。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemoveTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
一个64位世界名称（WWN），唯一标识应该从其事件报告给 WMI 客户端的端口列表中删除的本地端口。 有关全球名称的讨论，请参阅 T11 委员会*光纤通道 HBA API*规范。

*DiscoveredPortWWN*   
一个 WWN，指示远程发现的端口，应从其事件报告给 WMI 客户端的端口列表中删除该端口。

*AllTargets*   
要停止报告的事件。 如果此成员为零，则 WMI 提供程序客户端将停止报告与*DiscoveredPortWWN*指示的端口关联的事件。 如果此成员不为零，则 WMI 提供程序将停止报告所有关联的事件。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**RemoveTarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removetarget_out)结构的**HBAStatus**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_EVENTCONTROL WMI 类](msfc-eventcontrol-wmi-class.md)。

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi （包括 Hbapiwmi、Hbaapi 或 Hbaapi）。</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**RemoveTarget\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removetarget_in)

[**RemoveTarget\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removetarget_out)

 

 







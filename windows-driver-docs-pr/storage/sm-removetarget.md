---
title: SM\_RemoveTarget 函数
description: SM\_RemoveTarget WMI 方法配置 WMI 提供程序，使其停止将与指示的目标关联的事件传递给 WMI 客户端。
ms.assetid: 9be2a40c-299a-4d92-b9a2-ef60eb6d90e9
keywords:
- SM_RemoveTarget 函数存储设备
topic_type:
- apiref
api_name:
- SM_RemoveTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7c1b05b21b799385f821fa961068c5dfbcf09562
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845471"
---
# <a name="sm_removetarget-function"></a>SM\_RemoveTarget 函数


SM\_RemoveTarget WMI 方法配置 WMI 提供程序，使其停止将与指示的目标关联的事件传递给 WMI 客户端。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_RemoveTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
一个64位世界名称（WWN），用于唯一标识应该从其事件报告给 WMI 客户端的端口列表中删除的本地端口。 有关全球名称的详细信息，请参阅 T11 委员会*光纤通道 HBA API*规范。

*DiscoveredPortWWN*   
一个全球通用名称（WWN），用于指示应从其事件报告给 WMI 客户端的端口列表中删除的远程发现端口。

*AllTargets*   
要停止报告的事件。 如果此成员为零，则 WMI 提供程序客户端将停止报告与 DiscoveredPortWWN 指示的端口关联的事件。 如果此成员为非零，则 WMI 提供程序将停止报告所有关联的事件。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SM\_RemoveTarget\_OUT 结构的 HBAStatus 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS\_SM\_EventControl WMI 类。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_RemoveTarget\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removetarget_in)

[**SM\_RemoveTarget\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removetarget_out)

 

 







---
title: SM\_AddTarget 函数
description: SM\_AddTarget WMI 方法将 WMI 提供程序配置为通知 WMI 客户端与所指示的目标相关联的事件。
ms.assetid: 78e19496-1eb0-4d05-8637-f2e6d123208b
keywords:
- SM_AddTarget 函数存储设备
topic_type:
- apiref
api_name:
- SM_AddTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 800cadec0c88d95eff0f2e6717d1b69840b77155
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842603"
---
# <a name="sm_addtarget-function"></a>SM\_AddTarget 函数


SM\_AddTarget WMI 方法将 WMI 提供程序配置为通知 WMI 客户端与所指示的目标相关联的事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_AddTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DomainPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
WMI 客户端将接收其事件的本地端口的全球名称（WWN）。

*DiscoveredPortWWN*   
一个全球通用名称（WWN），指定 WMI 客户端将接收其事件的发现目标。

*DomainPortWWN*   
指定 WMI 客户端将接收其事件的本地端口的 SAS 域的全球名称（WWN）。

*AllTargets*   
要报告的目标事件的范围。 如果此成员为零，则 WMI 客户端将接收与 DiscoveredPortWWN 指示的端口关联的事件。 如果此成员为非零，则 WMI 客户端将接收与所有当前发现的目标以及将来发现的目标关联的所有事件。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SM\_AddTarget\_OUT 结构的 HBAStatus 成员中返回此信息。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_AddTarget\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addtarget_in)

[**SM\_AddTarget\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addtarget_out)

 

 







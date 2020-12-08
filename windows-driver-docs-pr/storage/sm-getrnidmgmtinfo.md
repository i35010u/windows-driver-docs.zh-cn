---
title: SM \_ GetRNIDMgmtInfo 函数
description: SM \_ GETRNIDMGMTINFO WMI 方法检索与光纤通道适配器关联的 FC3 管理信息。
keywords:
- SM_GetRNIDMgmtInfo 函数存储设备
topic_type:
- apiref
api_name:
- SM_GetRNIDMgmtInfo
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a81f679d94f334d56211f70aaadbfa058b0a30d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821828"
---
# <a name="sm_getrnidmgmtinfo-function"></a>SM \_ GetRNIDMgmtInfo 函数


SM \_ GETRNIDMGMTINFO WMI 方法检索与光纤通道适配器关联的 FC3 管理信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_GetRNIDMgmtInfo(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [out] HBAFC3MgmtInfo                    MgmtInfo
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
一个指示操作状态的 WMI 限定符值。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SM \_ GetRNIDMgmtInfo OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

*MgmtInfo*   
HBAFC3MgmtInfo 类型的结构，用于保存与光纤通道适配器关联的 FC3 管理信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS \_ SM \_ FabricAndDomainManagementMethods WMI 类。

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
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**SM \_ GetRNIDMgmtInfo \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getrnidmgmtinfo_out)

 


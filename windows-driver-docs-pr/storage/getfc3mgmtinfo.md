---
title: GetFC3MgmtInfo 函数
description: GetFC3MgmtInfo WMI 方法检索与光纤通道适配器关联的 FC3 管理信息。
keywords:
- GetFC3MgmtInfo 函数存储设备
topic_type:
- apiref
api_name:
- GetFC3MgmtInfo
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e43a1dbc20be1da5fa45d372327be7a8dd5920c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804563"
---
# <a name="getfc3mgmtinfo-function"></a>GetFC3MgmtInfo 函数


**GetFC3MgmtInfo** WMI 方法检索与光纤通道适配器关联的 FC3 管理信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFC3MgmtInfo(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [out] HBAFC3MgmtInfo                    MgmtInfo
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，将包含一个 WMI 限定符值，该值指示操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**GetFC3MgmtInfo \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc3mgmtinfo_out)结构的 **HBAStatus** 成员中返回此信息。

*MgmtInfo*   
返回时，包含 [**HBAFC3MgmtInfo**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo) 类型的结构，该结构包含与光纤通道适配器关联的 FC3 管理信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 [MSFC \_ HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetFC3MgmtInfo \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc3mgmtinfo_out)

[**HBAFC3MgmtInfo**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)

 


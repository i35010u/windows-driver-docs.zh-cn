---
title: SetFC3MgmtInfo 函数
description: SetFC3MgmtInfo WMI 方法设置与光纤通道适配器关联的 FC3 管理信息。
ms.assetid: 180f9945-3b2e-494e-8e6d-648ff4369c3b
keywords:
- SetFC3MgmtInfo 函数存储设备
topic_type:
- apiref
api_name:
- SetFC3MgmtInfo
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4e01f92bd4088f02ee8f04dd5b2b00655dbf3a67
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189675"
---
# <a name="setfc3mgmtinfo-function"></a>SetFC3MgmtInfo 函数


**SetFC3MgmtInfo** WMI 方法设置与光纤通道适配器关联的 FC3 管理信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SetFC3MgmtInfo(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in] HBAFC3MgmtInfo                     MgmtInfo
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**SetFC3MgmtInfo \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_out)结构的**HBAStatus**成员中返回此信息。

*MgmtInfo*   
[**HBAFC3MgmtInfo**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)类型的结构，该结构包含将用于配置光纤通道适配器的 FC3 管理信息。 此信息将传送到结构[** \_ 中 SetFC3MgmtInfo**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_in)的**PortWWN**成员中的微型端口驱动程序。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>注解
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
<td align="left"><p>Header</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**GetFC3MgmtInfo \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc3mgmtinfo_out)

[**HBAFC3MgmtInfo**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)

[**SetFC3MgmtInfo \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_in)

[**SetFC3MgmtInfo \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_out)

 


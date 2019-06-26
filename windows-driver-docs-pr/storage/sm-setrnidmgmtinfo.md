---
title: SM\_SetRNIDMgmtInfo 函数
description: SM\_SetRNIDMgmtInfo WMI 方法设置与光纤通道适配器相关联的 FC3 管理信息。
ms.assetid: 235beb52-0e09-402d-ace1-0543ad3ee74f
keywords:
- SM_SetRNIDMgmtInfo 函数存储设备
topic_type:
- apiref
api_name:
- SM_SetRNIDMgmtInfo
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 187662bb7d88a18b4ca8d128a1846f0813e3bacb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376885"
---
# <a name="smsetrnidmgmtinfo-function"></a>SM\_SetRNIDMgmtInfo 函数


SM\_SetRNIDMgmtInfo WMI 方法设置与光纤通道适配器相关联的 FC3 管理信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SetRNIDMgmtInfo(
   [in] HBAFC3MgmtInfo                     MgmtInfo,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>Parameters
----------

*MgmtInfo*   
类型 HBAFC3MgmtInfo 保存 FC3 与光纤通道适配器相关联的管理信息的结构。

*HBAStatus*   
一个 WMI 限定符值，该值指示操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_GetRNIDMgmtInfo\_结构。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS\_SM\_FabricAndDomainManagementMethods WMI 类。

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

[**SM\_SetRNIDMgmtInfo\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_setrnidmgmtinfo_in)

[**SM\_SetRNIDMgmtInfo\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_setrnidmgmtinfo_out)

 

 







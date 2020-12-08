---
title: SetFC3MgmtInfo 函数
description: SetFC3MgmtInfo WMI 方法设置与光纤通道适配器关联的 FC3 管理信息。
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
ms.openlocfilehash: 28db0d4a56cbad00e6991ccec9c5a465f6b617c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782092"
---
# <a name="setfc3mgmtinfo-function"></a>SetFC3MgmtInfo 函数


**SetFC3MgmtInfo** WMI 方法设置与光纤通道适配器关联的 FC3 管理信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SetFC3MgmtInfo(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in] HBAFC3MgmtInfo                     MgmtInfo
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**SetFC3MgmtInfo \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_out)结构的 **HBAStatus** 成员中返回此信息。

*MgmtInfo*   
[**HBAFC3MgmtInfo**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)类型的结构，该结构包含将用于配置光纤通道适配器的 FC3 管理信息。 此信息将传送到结构 [**\_ 中 SetFC3MgmtInfo**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_in)的 **PortWWN** 成员中的微型端口驱动程序。

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


[HBA \_ 状态](hba-status.md)

[**GetFC3MgmtInfo \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc3mgmtinfo_out)

[**HBAFC3MgmtInfo**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo)

[**SetFC3MgmtInfo \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_in)

[**SetFC3MgmtInfo \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setfc3mgmtinfo_out)

 


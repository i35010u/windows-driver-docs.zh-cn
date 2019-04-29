---
title: GetFC3MgmtInfo 函数
description: GetFC3MgmtInfo WMI 方法检索与光纤通道适配器相关联的 FC3 管理信息。
ms.assetid: dea5d73f-22e2-4c5e-973a-aa8407955ef8
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
ms.openlocfilehash: ee4a9079fb680385b6c1982ef53e92f0aeabafd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383137"
---
# <a name="getfc3mgmtinfo-function"></a>GetFC3MgmtInfo 函数


**GetFC3MgmtInfo** WMI 方法检索与光纤通道适配器相关联的 FC3 管理信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFC3MgmtInfo(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [out] HBAFC3MgmtInfo                    MgmtInfo
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含 WMI 限定符值，该值指示操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetFC3MgmtInfo\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff553946)结构。

*MgmtInfo*   
在返回时包含类型的结构[ **HBAFC3MgmtInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556032)保存 FC3 与光纤通道适配器相关联的管理信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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
<td align="left">Hbapiwmi.h （包括 Hbapiwmi.h、 Hbaapi.h 或 Hbaapi.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetFC3MgmtInfo\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff553946)

[**HBAFC3MgmtInfo**](https://msdn.microsoft.com/library/windows/hardware/ff556032)

 

 







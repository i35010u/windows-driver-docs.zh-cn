---
title: GetDiscoveredPortAttributes 函数
description: GetDiscoveredPortAttributes WMI 方法检索指定的远程光纤通道端口的属性。
ms.assetid: f71a02cf-035a-4de2-bb28-e1141a92795c
keywords:
- GetDiscoveredPortAttributes 函数存储设备
topic_type:
- apiref
api_name:
- GetDiscoveredPortAttributes
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fde95e3872e481915bdfd6ee6cc7c61e9e051b86
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383141"
---
# <a name="getdiscoveredportattributes-function"></a>GetDiscoveredPortAttributes 函数


**GetDiscoveredPortAttributes** WMI 方法检索指定的远程光纤通道端口的属性。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetDiscoveredPortAttributes(
   [in] uint32                                                        PortIndex,
   [in] uint32                                                        DiscoveredPortIndex,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                            HBAStatus,
   [out, HBAType("HBA_PORTATTRIBUTES")] MSFC_HBAPortAttributesResults PortAttributes
);
```

<a name="parameters"></a>Parameters
----------

*PortIndex*   
索引类型 Nx 的本地端口\_用来查询已发现的远程端口的端口。 此信息传递到中的微型端口驱动程序**PortIndex**的成员[ **GetDiscoveredPortAttributes\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff553927)结构。

*DiscoveredPortIndex*   
要查询的远程端口的索引。 此信息传递到中的微型端口驱动程序**DiscoveredPortIndex**的成员[ **GetDiscoveredPortAttributes\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff553927)结构。

*HBAStatus*   
在返回时包含 WMI 限定符值，该值指示操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetDiscoveredPortAttributes\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff553930)结构。

*PortAttributes*   
类型的结构[ **MSFC\_HBAPortAttributesResults** ](https://msdn.microsoft.com/library/windows/hardware/ff562510)中的哪些属性发现 FC\_端口可能会返回。 微型端口驱动程序将返回此信息**PortAttributes**的成员[ **GetDiscoveredPortAttributes\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff553930)结构。

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
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetDiscoveredPortAttributes\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff553927)

[**GetDiscoveredPortAttributes\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff553930)

[**MSFC\_HBAPortAttributesResults**](https://msdn.microsoft.com/library/windows/hardware/ff562510)

 

 







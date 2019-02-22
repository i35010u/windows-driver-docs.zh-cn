---
title: GetPortAttributesByWWN 函数
description: GetPortAttributesByWWN 方法检索由端口名称指定的端口的属性。
ms.assetid: 24b62b1c-9f47-40f1-aa72-849fabcbfbae
keywords:
- GetPortAttributesByWWN 函数存储设备
topic_type:
- apiref
api_name:
- GetPortAttributesByWWN
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1109369b42d33c9430b166631c1ed2095b9bc067
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525914"
---
# <a name="getportattributesbywwn-function"></a>GetPortAttributesByWWN 函数


**GetPortAttributesByWWN**方法检索由端口名称指定的端口的属性。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetPortAttributesByWWN(
   [in, HBAType("HBA_WWN")] uint8                                     wwn[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                            HBAStatus,
   [out, HBAType("HBA_PORTATTRIBUTES")] MSFC_HBAPortAttributesResults PortAttributes
);
```

<a name="parameters"></a>参数
----------

*wwn\[8\]*   
其属性是要查询的端口的名称。 此信息传递到中的微型端口驱动程序**wwn**的成员[ **GetPortAttributesByWWN\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff554967)结构。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetPortAttributesByWWN\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff554969)结构。

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
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi.h （包括 Hbapiwmi.h、 Hbaapi.h 或 Hbaapi.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetPortAttributesByWWN\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff554967)

[**GetPortAttributesByWWN\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff554969)

[**MSFC\_HBAPortAttributesResults**](https://msdn.microsoft.com/library/windows/hardware/ff562510)

 

 







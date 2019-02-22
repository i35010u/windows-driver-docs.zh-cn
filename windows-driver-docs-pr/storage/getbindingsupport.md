---
title: GetBindingSupport 函数
description: GetBindingSupport 方法检索当前已启用为所指示的端口的绑定功能。
ms.assetid: 50c90379-613f-42f1-80fe-7bc1b77a53bf
keywords:
- GetBindingSupport 函数存储设备
topic_type:
- apiref
api_name:
- GetBindingSupport
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8fd761893d6c2fbc3b44f2d3b116c3abcb1fd62d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542977"
---
# <a name="getbindingsupport-function"></a>GetBindingSupport 函数


**GetBindingSupport**方法检索当前已启用为所指示的端口的绑定功能。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetBindingSupport(
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [out, HBA_BIND_TYPE_QUALIFIERS] HBA_BIND_TYPE BindType
);
```

<a name="parameters"></a>参数
----------

*PortWWN\[8\]*   
指示将检索其永久绑定的端口的全球通用名称。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetBindingSupport\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff553917)结构。

*BindType*   
指示 HBA 的功能和其微型端口驱动程序提供一组特定的永久性绑定与相关的功能的位图。 此参数可以具有的值的列表，请参阅的说明[HBA\_绑定\_类型](hba-bind-type.md)WMI 类限定符。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

这**GetBindingSupport**方法返回当前已启用的绑定功能，而[ **GetBindingCapability** ](getbindingcapability.md)方法指示绑定而无需引用特定的绑定是否启用该端口的功能。

此 WMI 方法属于[MSFC\_HBAFCPInfo WMI 类](msfc-hbafcpinfo-wmi-class.md)。

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


[**GetBindingCapability**](getbindingcapability.md)

[**GetBindingSupport**](getbindingsupport.md)

[**GetBindingSupport\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff553914)

[**GetBindingSupport\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff553917)

 

 







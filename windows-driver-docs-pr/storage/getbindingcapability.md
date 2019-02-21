---
title: GetBindingCapability 函数
description: GetBindingCapability 方法检索所指示的端口的绑定功能。
ms.assetid: 8db1a3cc-5b79-4de9-a4cd-c75ac72c3785
keywords:
- GetBindingCapability 函数存储设备
topic_type:
- apiref
api_name:
- GetBindingCapability
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 44aa24a74b71830c91f2db5e68d31f627ade96bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544580"
---
# <a name="getbindingcapability-function"></a>GetBindingCapability 函数


**GetBindingCapability**方法检索所指示的端口的绑定功能。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetBindingCapability(
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
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetBindingCapability\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff553907)结构。

*BindType*   
指示 HBA 的功能和其微型端口驱动程序提供一组特定的永久性绑定与相关的功能。 此参数可以具有的值的列表，请参阅的说明[HBA\_绑定\_类型](hba-bind-type.md)WMI 类限定符。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

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


[**GetBindingCapability\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff553905)

[**GetBindingCapability\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff553907)

 

 







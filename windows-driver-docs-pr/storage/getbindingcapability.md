---
title: GetBindingCapability 函数
description: GetBindingCapability 方法检索所指示的端口的绑定功能。
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
ms.openlocfilehash: 3feb8485ca8c8f1dc38d5e8f6afce237860e0179
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804569"
---
# <a name="getbindingcapability-function"></a>GetBindingCapability 函数


**GetBindingCapability** 方法检索所指示的端口的绑定功能。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetBindingCapability(
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [out, HBA_BIND_TYPE_QUALIFIERS] HBA_BIND_TYPE BindType
);
```

<a name="parameters"></a>参数
----------

*PortWWN \[ 8\]*   
一个全球名称，指示要检索其持久性绑定的端口。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**GetBindingCapability \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getbindingcapability_out)结构的 **HBAStatus** 成员中返回此信息。

*BindType*   
指示 HBA 及其小型端口驱动程序提供与永久性绑定相关的一组特定功能的能力。 有关此参数可以具有的值的列表，请参阅 [HBA \_ 绑定 \_ 类型](hba-bind-type.md) WMI 类限定符的说明。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 [MSFC \_ HBAFCPInfo WMI 类](msfc-hbafcpinfo-wmi-class.md)。

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
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetBindingCapability \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getbindingcapability_in)

[**GetBindingCapability \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getbindingcapability_out)

 


---
title: GetBindingSupport 函数
description: GetBindingSupport 方法检索当前为指定端口启用的绑定功能。
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
ms.openlocfilehash: 1cb462f87b521ca83e316ace0d68eec018371938
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837851"
---
# <a name="getbindingsupport-function"></a>GetBindingSupport 函数


**GetBindingSupport**方法检索当前为指定端口启用的绑定功能。

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
一个全球名称，指示要检索其持久性绑定的端口。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**GetBindingSupport\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getbindingsupport_out)结构的**HBAStatus**成员中返回此信息。

*BindType*   
指示 HBA 及其微型端口驱动程序提供与永久性绑定相关的一组特定功能的位图。 有关此参数可以具有的值的列表，请参阅\_类型 WMI 类限定符[\_绑定 HBA](hba-bind-type.md)的说明。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此**GetBindingSupport**方法将返回当前启用的绑定功能，而[**GetBindingCapability**](getbindingcapability.md)方法指示该端口的绑定功能，而无需引用是否启用特定的绑定。

此 WMI 方法属于[MSFC\_HBAFCPINFO WMI 类](msfc-hbafcpinfo-wmi-class.md)。

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
<td align="left">Hbapiwmi （包括 Hbapiwmi、Hbaapi 或 Hbaapi）。</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetBindingCapability**](getbindingcapability.md)

[**GetBindingSupport**](getbindingsupport.md)

[**GetBindingSupport\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getbindingsupport_in)

[**GetBindingSupport\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getbindingsupport_out)

 

 







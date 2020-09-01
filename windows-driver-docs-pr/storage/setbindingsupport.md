---
title: SetBindingSupport 函数
description: SetBindingSupport 方法设置当前为指定端口启用的绑定功能。
ms.assetid: 52a469df-b184-460b-b515-a0b6eb946f1f
keywords:
- SetBindingSupport 函数存储设备
topic_type:
- apiref
api_name:
- SetBindingSupport
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d9bebcc7e4f2aba5a1fa0c8706eff0ee60097e74
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189687"
---
# <a name="setbindingsupport-function"></a>SetBindingSupport 函数


**SetBindingSupport**方法设置当前为指定端口启用的绑定功能。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SetBindingSupport(
   [in, HBAType("HBA_WWN")] uint8               PortWWN[8],
   [in, HBA_BIND_TYPE_QUALIFIERS] HBA_BIND_TYPE BindType,
   [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS     HBAStatus
);
```

<a name="parameters"></a>参数
----------

*PortWWN*   
一个全球名称，指示要检索其持久性绑定的端口。

*BindType*   
指示 HBA 及其微型端口驱动程序提供与永久性绑定相关的一组特定功能的位图。 有关此参数可以具有的值的列表，请参阅 [HBA \_ 绑定 \_ 类型](hba-bind-type.md) WMI 类限定符的说明。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**SetBindingSupport \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setbindingsupport_out)结构的**HBAStatus**成员中返回此信息。

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
<td align="left">“桌面”</td>
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


[**SetBindingSupport**](setbindingsupport.md)

[**SetBindingSupport \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setbindingsupport_in)

[**SetBindingSupport \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setbindingsupport_out)

 


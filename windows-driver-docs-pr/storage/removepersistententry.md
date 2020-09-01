---
title: RemovePersistentEntry 函数
description: RemovePersistentEntry 方法从与所指示的端口关联的绑定列表中删除绑定。
ms.assetid: f192367e-2e17-44e4-aa0b-7d23cd828b11
keywords:
- RemovePersistentEntry 函数存储设备
topic_type:
- apiref
api_name:
- RemovePersistentEntry
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3358acfb2e15ee8e0565a2bf8e4faa2b0f0f3e64
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189223"
---
# <a name="removepersistententry-function"></a>RemovePersistentEntry 函数


**RemovePersistentEntry**方法从与所指示的端口关联的绑定列表中删除绑定。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemovePersistentEntry(
   [in, HBAType("HBA_WWN")] uint8                            PortWWN[8],
   [in, HbaType("HBA_FCPBINDINGENTRY2")] HBAFCPBindingEntry2 Binding,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                   HBAStatus
);
```

<a name="parameters"></a>参数
----------

*PortWWN*   
一个全球名称，它指示将更改其持久性绑定的端口。

*Binding*   
[**HBAFCPBindingEntry2**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)类型的结构，指示要从指示的端口的绑定列表中移除的绑定。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**RemovePersistentEntry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removepersistententry_out)结构的**HBAStatus**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>注解
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
<td align="left"><p>Header</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**RemovePersistentEntry \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removepersistententry_in)

[**RemovePersistentEntry \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removepersistententry_out)

 


---
title: SetPersistentEntry 函数
description: SetPersistentEntry 方法将绑定添加到与所指示的端口关联的绑定列表。
keywords:
- SetPersistentEntry 函数存储设备
topic_type:
- apiref
api_name:
- SetPersistentEntry
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4d02206024ba85048d513ad767afba7036eb4f2b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811411"
---
# <a name="setpersistententry-function"></a>SetPersistentEntry 函数


**SetPersistentEntry** 方法将绑定添加到与所指示的端口关联的绑定列表。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SetPersistentEntry(
   [in, HBAType("HBA_WWN")] uint8                            PortWWN[8],
   [in, HbaType("HBA_FCPBINDINGENTRY2")] HBAFCPBindingEntry2 Binding,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                   HBAStatus
);
```

<a name="parameters"></a>参数
----------

*PortWWN*   
一个全球名称，它指示将更改其持久性绑定的端口。

*Binding*   
[**HBAFCPBindingEntry2**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)类型的结构，指示要从指示的端口的绑定列表中移除的绑定。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**SetPersistentEntry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setpersistententry_out)结构的 **HBAStatus** 成员中返回此信息。

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
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**SetPersistentEntry \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setpersistententry_in)

[**SetPersistentEntry \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setpersistententry_out)

 


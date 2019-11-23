---
title: SetPersistentEntry 函数
description: SetPersistentEntry 方法将绑定添加到与所指示的端口关联的绑定列表。
ms.assetid: 52680641-9f63-4c8e-9538-4c725b9074a3
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
ms.openlocfilehash: 6a39ca2923d7f5b7e3fad4db351df763fe42d707
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840469"
---
# <a name="setpersistententry-function"></a>SetPersistentEntry 函数


**SetPersistentEntry**方法将绑定添加到与所指示的端口关联的绑定列表。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SetPersistentEntry(
   [in, HBAType("HBA_WWN")] uint8                            PortWWN[8],
   [in, HbaType("HBA_FCPBINDINGENTRY2")] HBAFCPBindingEntry2 Binding,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                   HBAStatus
);
```

<a name="parameters"></a>参数
----------

*PortWWN*   
一个全球名称，它指示将更改其持久性绑定的端口。

*绑定*   
[**HBAFCPBindingEntry2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)类型的结构，指示要从指示的端口的绑定列表中移除的绑定。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**SetPersistentEntry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setpersistententry_out)结构的**HBAStatus**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

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
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**SetPersistentEntry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setpersistententry_in)

[**SetPersistentEntry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_setpersistententry_out)

 

 







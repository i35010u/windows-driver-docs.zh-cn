---
title: RemovePersistentEntry 函数
description: RemovePersistentEntry 方法从与指定的端口相关联的绑定的列表中删除绑定。
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
ms.openlocfilehash: af5f25f15372845c46293af3f925175633df1a69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522604"
---
# <a name="removepersistententry-function"></a>RemovePersistentEntry 函数


**RemovePersistentEntry**方法从与指定的端口相关联的绑定的列表中删除绑定。

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
指示将更改其永久绑定的端口的全球通用名称。

*绑定*   
类型的结构[ **HBAFCPBindingEntry2** ](https://msdn.microsoft.com/library/windows/hardware/ff556035) ，该值指示要从绑定的指定的端口的列表中移除的绑定。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **RemovePersistentEntry\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff563994)结构。

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
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**RemovePersistentEntry\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff563990)

[**RemovePersistentEntry\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff563994)

 

 







---
title: GetPersistentBinding2 函数
description: GetPersistentBinding2 方法检索 HBA 微型端口驱动程序用来将其逻辑单元标识为逻辑单元的光纤通道协议 (FCP) 标识符的绑定。
ms.assetid: 17734973-fa82-4f54-b882-d9a2f5ce2066
keywords:
- GetPersistentBinding2 函数存储设备
topic_type:
- apiref
api_name:
- GetPersistentBinding2
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c32bbd54dace18375d8f5e384885e79e0481449a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193209"
---
# <a name="getpersistentbinding2-function"></a>GetPersistentBinding2 函数


**GetPersistentBinding2**方法检索 HBA 微型端口驱动程序用来将其逻辑单元标识为逻辑单元的光纤通道协议 (FCP) 标识符的绑定。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetPersistentBinding2(
   [in, HBAType("HBA_WWN")] uint8                        PortWWN[8],
   [in] uint32                                           InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS               HBAStatus,
   [out] uint32                                          TotalEntryCount,
   [out] uint32                                          OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] HBAFCPBindingEntry2 Bindings[]
);
```

<a name="parameters"></a>参数
----------

*PortWWN \[ 8\]*   
一个全球名称，指示要检索其持久性绑定的端口。

*InEntryCount*   
指示 WMI 提供程序可以在 *输入* 参数中报告的绑定项的数目。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**GetFcpPersistentBinding \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)结构的**HBAStatus**成员中返回此信息。

*TotalEntryCount*   
指示与 HBA 关联的永久性绑定的总数。

*OutEntryCount*   
指示 **GetPersistentBinding2** 方法检索的持久绑定的总数。 此值将小于或等于 *TotalEntryCount*。

*绑定\[\]*   
[**HBAFCPBindingEntry2**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)类型的结构的数组，这些结构描述了操作系统与光纤通道协议之间的 HBA 绑定 (FCP) 标识符。

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


[**GetFcpPersistentBinding \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_in)

[**GetFcpPersistentBinding \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)

[**HBAFCPBindingEntry2**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)

 


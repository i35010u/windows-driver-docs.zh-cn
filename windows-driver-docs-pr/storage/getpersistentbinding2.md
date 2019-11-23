---
title: GetPersistentBinding2 函数
description: GetPersistentBinding2 方法检索 HBA 微型端口驱动程序用来映射信息的绑定，操作系统使用这些信息来将其逻辑单元标识为逻辑单元的光纤通道协议（FCP）标识符。
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
ms.openlocfilehash: 42113e99635b85e419f902cac0cb8b44f1b255be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844690"
---
# <a name="getpersistentbinding2-function"></a>GetPersistentBinding2 函数


**GetPersistentBinding2**方法检索 HBA 微型端口驱动程序用来映射信息的绑定，操作系统使用这些信息来将其逻辑单元标识为逻辑单元的光纤通道协议（FCP）标识符。

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

*PortWWN\[8\]*    
一个全球名称，指示要检索其持久性绑定的端口。

*InEntryCount*   
指示 WMI 提供程序可以在*输入*参数中报告的绑定项的数目。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**GetFcpPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)结构的**HBAStatus**成员中返回此信息。

*TotalEntryCount*   
指示与 HBA 关联的永久性绑定的总数。

*OutEntryCount*   
指示**GetPersistentBinding2**方法检索的持久绑定的总数。 此值将小于或等于*TotalEntryCount*。

*绑定\[\]*    
[**HBAFCPBindingEntry2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)类型的结构的数组，这些结构描述了操作系统与光纤通道协议（FCP）标识符之间的 HBA 绑定。

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


[**GetFcpPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_in)

[**GetFcpPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)

[**HBAFCPBindingEntry2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)

 

 







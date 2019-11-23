---
title: GetFcpPersistentBinding 函数
description: GetFcpPersistentBinding 方法检索 HBA 微型端口驱动程序用来映射信息的绑定，操作系统使用这些信息来将其逻辑单元标识为逻辑单元的光纤通道协议（FCP）标识符。
ms.assetid: ee675022-51f7-4b81-863c-ee608b0284b0
keywords:
- GetFcpPersistentBinding 函数存储设备
topic_type:
- apiref
api_name:
- GetFcpPersistentBinding
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 36cf385cd3c462837cb6f6c4327a3494e2505446
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837964"
---
# <a name="getfcppersistentbinding-function"></a>GetFcpPersistentBinding 函数


**GetFcpPersistentBinding**方法检索 HBA 微型端口驱动程序用来映射信息的绑定，操作系统使用这些信息来将其逻辑单元标识为逻辑单元的光纤通道协议（FCP）标识符。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFcpPersistentBinding(
   [in] uint32                                          InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS              HBAStatus,
   [out] uint32                                         TotalEntryCount,
   [out] uint32                                         OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] HBAFCPBindingEntry Entry[]
);
```

<a name="parameters"></a>参数
----------

*InEntryCount*   
指示 WMI 提供程序可以在*输入*参数中报告的绑定项的数目。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**GetFcpPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)结构的**HBAStatus**成员中返回此信息。

*TotalEntryCount*   
指示与 HBA 关联的永久性绑定的总数。

*OutEntryCount*   
指示**GetFcpPersistentBinding**方法检索的永久性绑定的总数。 此值将小于或等于*TotalEntryCount*。

*条目\[\]*    
[**HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)类型的结构的数组，这些结构描述了操作系统与光纤通道协议（FCP）标识符之间的 HBA 绑定。

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
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetFcpPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_in)

[**GetFcpPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)

[**HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)

 

 







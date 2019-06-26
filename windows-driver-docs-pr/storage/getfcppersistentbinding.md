---
title: GetFcpPersistentBinding 函数
description: GetFcpPersistentBinding 方法检索的绑定 HBA 微型端口驱动程序用来将映射操作系统用来识别其逻辑单元与光纤通道协议 (FCP) 标识符的逻辑单元的信息。
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
ms.openlocfilehash: 9d29af748b40b47e5143c81f5b006a4d714d90f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378539"
---
# <a name="getfcppersistentbinding-function"></a>GetFcpPersistentBinding 函数


**GetFcpPersistentBinding**方法检索 HBA 微型端口驱动程序用来映射信息操作系统用来标识其逻辑单元的光纤通道协议 (FCP) 标识符与绑定逻辑单元。

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

<a name="parameters"></a>Parameters
----------

*InEntryCount*   
指示 WMI 提供程序可以报告中的绑定项数*条目*参数。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetFcpPersistentBinding\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)结构。

*TotalEntryCount*   
指示与 HBA 相关联的持久绑定的总数。

*OutEntryCount*   
指示永久性来检索的绑定的总数**GetFcpPersistentBinding**方法。 此值将为小于或等于*TotalEntryCount*。

*条目\[\]*    
类型的结构数组[ **HBAFCPBindingEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry) ，描述操作系统与光纤通道协议 (FCP) 标识符之间的 HBA 的绑定。

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
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi.h （包括 Hbapiwmi.h、 Hbaapi.h 或 Hbaapi.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetFcpPersistentBinding\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_in)

[**GetFcpPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)

[**HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)

 

 







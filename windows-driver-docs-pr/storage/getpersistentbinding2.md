---
title: GetPersistentBinding2 函数
description: GetPersistentBinding2 方法检索的绑定 HBA 微型端口驱动程序用来将映射操作系统用来识别其逻辑单元与光纤通道协议 (FCP) 标识符的逻辑单元的信息。
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
ms.openlocfilehash: bc0e194e94ab886f8aae1632dc990bca8f412cc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521768"
---
# <a name="getpersistentbinding2-function"></a>GetPersistentBinding2 函数


**GetPersistentBinding2**方法检索 HBA 微型端口驱动程序用来映射信息操作系统用来标识其逻辑单元的光纤通道协议 (FCP) 标识符与绑定逻辑单元。

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
指示将检索其永久绑定的端口的全球通用名称。

*InEntryCount*   
指示 WMI 提供程序可以报告中的绑定项数*条目*参数。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetFcpPersistentBinding\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff554936)结构。

*TotalEntryCount*   
指示与 HBA 相关联的持久绑定的总数。

*OutEntryCount*   
指示永久性来检索的绑定的总数**GetPersistentBinding2**方法... 此值将为小于或等于*TotalEntryCount*。

*绑定\[\]*   
类型的结构数组[ **HBAFCPBindingEntry2** ](https://msdn.microsoft.com/library/windows/hardware/ff556035) ，描述操作系统与光纤通道协议 (FCP) 标识符之间的 HBA 的绑定。

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


[**GetFcpPersistentBinding\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff554933)

[**GetFcpPersistentBinding\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff554936)

[**HBAFCPBindingEntry2**](https://msdn.microsoft.com/library/windows/hardware/ff556035)

 

 







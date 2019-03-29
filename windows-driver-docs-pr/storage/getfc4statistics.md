---
title: GetFC4Statistics 函数
description: GetFC4Statistics WMI 方法报告类型 Nx 的端口上的流量统计数据\_所指示的 FC 4 协议端口。
ms.assetid: f57f11bf-57b8-4ae9-96b3-4191f412c80c
keywords:
- GetFC4Statistics 函数存储设备
topic_type:
- apiref
api_name:
- GetFC4Statistics
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b420920bf57c4a27de06a54abe86adc2410ddad3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562858"
---
# <a name="getfc4statistics-function"></a>GetFC4Statistics 函数


**GetFC4Statistics** WMI 方法报告类型 Nx 的端口上的流量统计数据\_所指示的 FC 4 协议端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFC4Statistics(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in, HBAType("HBA_WWN")] uint8          PortWWN,
   [in] uint8                              FC4Type,
   [out] MSFC_FC4STATISTICS                FC4Statistics
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含 WMI 限定符值，该值指示操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetFC4Statistics\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff553960)结构。

*PortWWN*   
类型 Nx 的本地端口的全球通用名称\_端口的流量统计信息是报告。 此信息传递到中的微型端口驱动程序**端口全球通用名称**的成员[ **GetFC4Statistics\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff553958)结构。

*FC4Type*   
一个值，指示类型 FC 4 协议。 FC4 类型的说明，请参阅 T11 委员会*光纤通道通用服务-4*规范。 此信息传递到中的微型端口驱动程序**FC4Type**的成员[ **GetFC4Statistics\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff553958)结构。

*FC4Statistics*   
在返回时包含类型的结构[ **MSFC\_FC4STATISTICS** ](https://msdn.microsoft.com/library/windows/hardware/ff562492)保存指定的 FC 4 协议的统计信息。 微型端口驱动程序将返回此信息**FC4Statistics**的成员[ **GetFC4Statistics\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff553960)结构。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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


[**GetFC4Statistics\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff553958)

[**GetFC4Statistics\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff553960)

[HBA\_状态](hba-status.md)

[**MSFC\_FC4STATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff562492)

 

 







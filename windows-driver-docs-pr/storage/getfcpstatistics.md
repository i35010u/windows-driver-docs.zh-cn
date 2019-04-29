---
title: GetFCPStatistics 函数
description: GetFCPStatistics WMI 方法返回所指示的 SCSI 逻辑单元上指示本地 HBA FCP 流量统计数据。
ms.assetid: 566368d7-ee13-449d-97c3-1c214984fee5
keywords:
- GetFCPStatistics 函数存储设备
topic_type:
- apiref
api_name:
- GetFCPStatistics
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 86c8b6a03b29267f97728e41e72e25aa54561c91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354039"
---
# <a name="getfcpstatistics-function"></a>GetFCPStatistics 函数


**GetFCPStatistics** WMI 方法返回 FCP 流量统计数据所指示的 SCSI 逻辑单元上指示本地 HBA。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFCPStatistics(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in] HBAScsiID                          ScsiId,
   [out] MSFC_FC4STATISTICS                FC4Statistics
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含 WMI 限定符值，该值指示操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetFCPStatistics\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff554944)结构。

*ScsiId*   
在返回时包含类型的结构[ **HBAScsiID** ](https://msdn.microsoft.com/library/windows/hardware/ff556042)保存标识设备的信息。 此信息传递到中的微型端口驱动程序**ScsiId**的成员[ **GetFCPStatistics\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff554942)结构。

*FC4Statistics*   
在返回时包含类型的结构[ **MSFC\_FC4STATISTICS** ](https://msdn.microsoft.com/library/windows/hardware/ff562492)用于保存所指示的 SCSI 逻辑单元的统计信息。 微型端口驱动程序将返回此信息**FC4Statistics**的成员[ **GetFCPStatistics\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff554944)结构。

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


[**GetFCPStatistics\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff554942)

[**GetFCPStatistics\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff554944)

[**MSFC\_FC4STATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff562492)

 

 







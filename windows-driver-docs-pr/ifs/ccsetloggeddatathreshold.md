---
title: CcSetLoggedDataThreshold 例程
description: CcSetLoggedDataThreshold 例程设置的阈值时的脏日志页扫描将启动延迟写入。
ms.assetid: 067121C3-3BD6-48EA-BD8E-B28620F799E1
keywords:
- CcSetLoggedDataThreshold 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- CcSetLoggedDataThreshold
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4c2d13ee49f2ba986f1ed04ac3d05c5b4720425
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368582"
---
# <a name="ccsetloggeddatathreshold-routine"></a>CcSetLoggedDataThreshold 例程


[ **CcSetLoggedDataThreshold** ](ccistheredirtyloggedpages.md)例程设置阈值时的脏日志页扫描将启动延迟写入。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID CcSetLoggedDataThreshold(
  _In_ PVOID LogHandle,
  _In_ ULONG NumberOfPages
);
```

<a name="parameters"></a>Parameters
----------

*LogHandle* \[in\]  
新阈值的日志句柄。

*NumberOfPages* \[in\]  
指定的日志的脏日志页中的阈值数量*LogHandle*。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

中的阈值值*页数*中返回的值时，才使用*PercentageUsed*参数*QueryLogUsageRoutine*回调例程为 0。 *QueryLogUsageRoutine*通过调用设置回拨[ **CcSetLogHandleForFileEx**](ccsetloghandleforfileex.md)。

[ **CcSetLoggedDataThreshold** ](ccistheredirtyloggedpages.md)使用例程时不使用日志完整百分比脏日志页面数设置为固定的值。

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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 8 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 FltKernel.h）</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**CcSetLogHandleForFileEx**](ccsetloghandleforfileex.md)

 

 







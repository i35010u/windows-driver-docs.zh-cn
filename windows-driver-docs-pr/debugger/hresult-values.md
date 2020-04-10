---
title: HRESULT 值
description: 下面列出了函数和方法的常见返回值及其常见含义。
ms.assetid: 713f3ee2-2f5b-415e-9908-90f5ae428b43
ms.date: 12/07/2017
keywords:
- HRESULT 值 Windows 调试
topic_type:
- apiref
api_name:
- HRESULT Values
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: b20726a1d9d65d37cc890337ceb3b12b898b741c
ms.sourcegitcommit: 329eee396e727bbd1b2a096a5c7bb0c4b78f52e5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2020
ms.locfileid: "81007809"
---
# <a name="hresult-values"></a>HRESULT 值


下面列出了函数和方法的常见返回值及其常见含义。

## <span id="ddk_return_values_dbx"></span><span id="DDK_RETURN_VALUES_DBX"></span>


**成功的结果。** 这些值是在 Winerror.h 中定义的。

<span id="S_OK"></span><span id="s_ok"></span>S\_确定  
成功完成。

<span id="S_FALSE"></span><span id="s_false"></span>S\_FALSE  
已完成，但未出现错误，但仅获取了部分结果。

如果缓冲区不够大，无法容纳返回的信息，则返回的信息通常会被截断以容纳到缓冲区中，并从方法返回\_FALSE。

**错误结果。** 这些值是在 Winerror.h 中定义的。

<span id="E_FAIL"></span><span id="e_fail"></span>E\_失败  
无法执行该操作。

<span id="E_INVALIDARG"></span><span id="e_invalidarg"></span>E\_INVALIDARG  
传入的参数之一无效。

<span id="E_NOINTERFACE"></span><span id="e_nointerface"></span>E\_NOINTERFACE  
找不到搜索的对象。

<span id="E_OUTOFMEMORY"></span><span id="e_outofmemory"></span>E\_OUTOFMEMORY  
内存分配尝试失败。

<span id="E_UNEXPECTED"></span><span id="e_unexpected"></span>E\_意外  
目标不可访问，或引擎未处于可处理函数或方法的状态。

<span id="E_NOTIMPL"></span><span id="e_notimpl"></span>E\_NOTIMPL  
未实现。

<span id="HRESULT_FROM_WIN32_ERROR_ACCESS_DENIED_"></span><span id="hresult_from_win32_error_access_denied_"></span>\_WIN32 中的 HRESULT\_（错误\_访问\_拒绝）  
由于调试器处于[安全模式](https://docs.microsoft.com/windows-hardware/drivers/debugger/secure-mode)，操作被拒绝。

**NT 错误结果。** 有时会出现其他错误代码（例如状态\_控制\_C\_退出和状态\_无\_更\_的条目）。 这些结果将从 Winerror.h 中定义的\_NT 宏传递到 HRESULT\_，然后再返回。

**Win32 错误结果。** 有时会出现其他错误代码（如错误\_读取\_错误和错误\_写入\_错误。 在返回之前，这些结果将从 Winerror.h 中定义的\_WIN32 宏传递到 HRESULT\_。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">DbgEng （包括 DbgEng）</td>
</tr>
</tbody>
</table>

 

 






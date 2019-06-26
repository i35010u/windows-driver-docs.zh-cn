---
title: HRESULT 值
description: 下面是常见的返回值的函数和方法，以及其常见的含义的列表。
ms.assetid: 713f3ee2-2f5b-415e-9908-90f5ae428b43
ms.date: 10/30/2017
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
ms.openlocfilehash: 810363c67df37c350560ed1b32b6fbf6253e7071
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361323"
---
# <a name="hresult-values"></a>HRESULT 值


下面是常见的返回值的函数和方法，以及其常见的含义的列表。

## <span id="ddk_return_values_dbx"></span><span id="DDK_RETURN_VALUES_DBX"></span>


**成功的结果。** 在 WinError.h 中定义这些值。

<span id="S_OK"></span><span id="s_ok"></span>S\_确定  
成功完成。

<span id="S_FALSE"></span><span id="s_false"></span>S\_FALSE  
完成，没有错误，但获得仅部分结果。

如果缓冲区足以容纳返回到它的信息，通常被返回的信息的截断以适合缓冲区和 S\_从方法返回 FALSE。

**错误结果。** 在 WinError.h 中定义这些值。

<span id="E_FAIL"></span><span id="e_fail"></span>E\_FAIL  
无法执行该操作。

<span id="E_INVALIDARG"></span><span id="e_invalidarg"></span>E\_INVALIDARG  
传入的参数之一无效。

<span id="E_NOINTERFACE"></span><span id="e_nointerface"></span>E\_NOINTERFACE  
找不到搜索的对象。

<span id="E_OUTOFMEMORY"></span><span id="e_outofmemory"></span>E\_OUTOFMEMORY  
内存分配失败。

<span id="E_UNEXPECTED"></span><span id="e_unexpected"></span>E\_UNEXPECTED  
目标不可访问，或引擎无法在函数或方法无法处理的状态。

<span id="E_NOTIMPL"></span><span id="e_notimpl"></span>E\_NOTIMPL  
未实现。

<span id="HRESULT_FROM_WIN32_ERROR_ACCESS_DENIED_"></span><span id="hresult_from_win32_error_access_denied_"></span>HRESULT\_FROM\_WIN32 (错误\_访问\_拒绝)  
该操作被拒绝，因为调试器处于[安全模式下](https://docs.microsoft.com/windows-hardware/drivers/debugger/secure-mode)。

**NT 错误结果。** 其他错误代码，如状态\_控制\_C\_退出和状态\_否\_详细\_条目，有时可以出现。 这些结果传递到 HRESULT\_FROM\_NT 在返回前在 WinError.h 中定义的宏。

**Win32 错误结果。** 其他错误代码，例如错误\_读取\_容错域和错误\_编写\_同时出现故障，有时可以。 这些结果传递到 HRESULT\_FROM\_在返回前在 WinError.h 中定义的 WIN32 宏。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h （包括 DbgEng.h）</td>
</tr>
</tbody>
</table>

 

 






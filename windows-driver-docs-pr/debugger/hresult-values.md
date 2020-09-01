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
ms.openlocfilehash: db6fa523be3e4a5629b937235ecdbc417130bd8e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210219"
---
# <a name="hresult-values"></a>HRESULT 值


下面列出了函数和方法的常见返回值及其常见含义。

## <span id="ddk_return_values_dbx"></span><span id="DDK_RETURN_VALUES_DBX"></span>


**成功的结果。** 这些值是在 Winerror.h 中定义的。

<span id="S_OK"></span><span id="s_ok"></span>S \_ 正常  
成功完成。

<span id="S_FALSE"></span><span id="s_false"></span>S \_ FALSE  
已完成，但未出现错误，但仅获取了部分结果。

如果缓冲区不够大，无法容纳返回的信息，则返回的信息通常会被截断以容纳到缓冲区中，并 \_ 从方法返回 S FALSE。

**错误结果。** 这些值是在 Winerror.h 中定义的。

<span id="E_FAIL"></span><span id="e_fail"></span>E \_ 失败  
无法执行该操作。

<span id="E_INVALIDARG"></span><span id="e_invalidarg"></span>E \_ INVALIDARG  
传入的参数之一无效。

<span id="E_NOINTERFACE"></span><span id="e_nointerface"></span>E \_ NOINTERFACE  
找不到搜索的对象。

<span id="E_OUTOFMEMORY"></span><span id="e_outofmemory"></span>E \_ OUTOFMEMORY  
内存分配尝试失败。

<span id="E_UNEXPECTED"></span><span id="e_unexpected"></span>E \_ 意外  
目标不可访问，或引擎未处于可处理函数或方法的状态。

<span id="E_NOTIMPL"></span><span id="e_notimpl"></span>E \_ NOTIMPL  
未实现。

<span id="HRESULT_FROM_WIN32_ERROR_ACCESS_DENIED_"></span><span id="hresult_from_win32_error_access_denied_"></span>HRESULT \_ 中的 HRESULT \_ (\_ 拒绝访问错误 \_)   
由于调试器处于 [安全模式](./secure-mode.md)，操作被拒绝。

**NT 错误结果。** 有时会出现其他错误代码，如状态 \_ 控制 \_ C \_ 退出和状态 \_ 不 \_ 多 \_ 项。 在 \_ 返回之前，将从 \_ winerror.h 中定义的 NT 宏将这些结果传递给 HRESULT。

**Win32 错误结果。** 有时会出现其他错误代码，如 "错误读取错误" \_ \_ 和 \_ "错误写入错误 \_ "。 在 \_ 返回之前，将从 \_ winerror.h 中定义的 WIN32 宏将这些结果传递给 HRESULT。

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
<td align="left">DbgEng (包含 DbgEng) </td>
</tr>
</tbody>
</table>

 


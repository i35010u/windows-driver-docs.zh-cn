---
title: 数据类型需要形式转换
description: 数据类型需要形式转换
ms.assetid: af1d7986-7bf2-4587-b487-91658e7a3b19
keywords:
- 形式转换 WDK
- WOW64 形式转换层 WDK
- 32 位 I/O 支持 WDK 64 位形式转换
- 数据类型 WDK 64 位
- 指针精确度 WDK 64 位
- 固定精度数据类型 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4f6ca86749a487a1d7bfd04abffa81793ffab29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520455"
---
# <a name="which-data-types-need-thunking"></a>数据类型需要形式转换





下表列出了需要形式转换，以及其 thunked 等效项的常见数据类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>指针精度数据类型 （之前形式转换）</th>
<th>（后形式转换） 的等效 32 位的固定精度数据类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>句柄</p></td>
<td><p>VOID * POINTER_32</p></td>
</tr>
<tr class="even">
<td><p>INT_PTR</p></td>
<td><p>INT32</p></td>
</tr>
<tr class="odd">
<td><p>LONG_PTR</p></td>
<td><p>LONG32</p></td>
</tr>
<tr class="even">
<td><p>LPARAM</p></td>
<td><p>LONG32</p></td>
</tr>
<tr class="odd">
<td><p>PCHAR</p></td>
<td><p>Char * POINTER_32</p></td>
</tr>
<tr class="even">
<td><p>PDWORD</p></td>
<td><p>DWORD * POINTER_32</p></td>
</tr>
<tr class="odd">
<td><p>PHANDLE</p></td>
<td><p>VOID * * POINTER_32</p></td>
</tr>
<tr class="even">
<td><p>PULONG</p></td>
<td><p>ULONG * POINTER_32</p></td>
</tr>
<tr class="odd">
<td><p>PVOID</p></td>
<td><p>VOID * POINTER_32</p></td>
</tr>
<tr class="even">
<td><p>PWORD</p></td>
<td><p>WORD * POINTER_32</p></td>
</tr>
<tr class="odd">
<td><p>SIZE_T</p></td>
<td><p>INT32</p></td>
</tr>
<tr class="even">
<td><p>ULONG_PTR</p></td>
<td><p>ULONG32</p></td>
</tr>
<tr class="odd">
<td><p>UNICODE_STRING</p></td>
<td><p>UNICODE_STRING32</p></td>
</tr>
</tbody>
</table>

 

 

 





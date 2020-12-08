---
title: 哪些数据类型需要形实转换
description: 哪些数据类型需要形实转换
keywords:
- thunk WDK
- WOW64 thunk 层 WDK
- 32位 i/o 支持 WDK 64 位，thunk
- 数据类型 WDK 64 位
- 指针精度 WDK 64 位
- 固定精度数据类型 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: da0a40f76b934a8e957eda8ea41fb778c4f28448
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832279"
---
# <a name="which-data-types-need-thunking"></a>哪些数据类型需要形实转换





下表列出了需要 thunk 的常见数据类型及其 thunked 等效项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Thunk 之前的指针精度数据类型 () </th>
<th>Thunk 后的等效32位固定精度数据类型 () </th>
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

 

 

 





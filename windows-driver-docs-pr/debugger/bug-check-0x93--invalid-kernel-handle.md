---
title: Bug 检查 0x93 INVALID_KERNEL_HANDLE
description: INVALID_KERNEL_HANDLE bug 检查具有 0x00000093 值。 此 bug 检查指示无效或受保护的句柄传递给 NtClose。
ms.assetid: c8564da7-cdbf-40f5-94f4-b1fac23b8b42
keywords:
- Bug 检查 0x93 INVALID_KERNEL_HANDLE
- INVALID_KERNEL_HANDLE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_KERNEL_HANDLE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e7bfb6a2d05a70d1f7c0f335a2e35070df745510
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520436"
---
# <a name="bug-check-0x93-invalidkernelhandle"></a>Bug 检查 0x93:无效\_内核\_处理


无效\_内核\_句柄 bug 检查的值为 0x00000093。 此 bug 检查指示无效或受保护的句柄传递给**NtClose**。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="invalidkernelhandle-parameters"></a>无效\_内核\_句柄参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>句柄传递给<strong>NtClose</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>调用方尝试关闭受保护的句柄</p>
<p><strong>1:</strong>调用方尝试关闭句柄无效</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

无效\_内核\_句柄 bug 检查指示某些内核代码 （例如，在服务器、 重定向程序或另一个驱动程序） 尝试关闭无效句柄或受保护的句柄。

 

 





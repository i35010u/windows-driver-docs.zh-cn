---
title: Bug 检查 0x190 WIN32K_CRITICAL_FAILURE_LIVEDUMP
description: WIN32K_CRITICAL_FAILURE_LIVEDUMP bug 检查具有 0x00000190 值。 这指示 Win32k 遇到严重故障。 捕获实时转储收集调试信息。
ms.assetid: 39C0145D-08FE-4BBC-A729-9E70198CF87F
keywords:
- Bug 检查 0x190 WIN32K_CRITICAL_FAILURE_LIVEDUMP
- WIN32K_CRITICAL_FAILURE_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WIN32K_CRITICAL_FAILURE_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe6645bff32dc3ed4f02afbc2a725215b40ec19f
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238352"
---
# <a name="bug-check-0x190-win32kcriticalfailurelivedump"></a>Bug 检查 0x190：WIN32K\_严重\_失败\_LIVEDUMP


WIN32K\_严重\_失败\_LIVEDUMP bug 检查的值为 0x00000190。 这指示 Win32k 遇到严重故障。 捕获实时转储收集调试信息。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="win32kcriticalfailurelivedump-parameters"></a>WIN32K\_严重\_失败\_LIVEDUMP 参数


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
<td align="left">1</td>
<td align="left"><p>失败的类型</p>
<p>0x1:REGION_VALIDATION_FAILURE 的区域是超出图面上的界限。</p>
2-指向 DC 3 的指针到区域的图面 4 指针
<p>0x2:OPERATOR_NEW_USED-"new"运算符用于分配内存。</p>
2-保留 3-保留 4-保留</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数 1</td>
</tr>
</tbody>
</table>

 

 

 





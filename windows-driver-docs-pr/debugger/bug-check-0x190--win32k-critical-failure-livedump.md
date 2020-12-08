---
title: Bug 检查 0x190 WIN32K_CRITICAL_FAILURE_LIVEDUMP
description: WIN32K_CRITICAL_FAILURE_LIVEDUMP bug 检查的值为0x00000190。 这表明 Win32k.sys 遇到了严重故障。 捕获实时转储以收集调试信息。
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
ms.openlocfilehash: 7324eb7ceb9f60c9e8b45c7676b9bc26ae7d3694
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814021"
---
# <a name="bug-check-0x190-win32k_critical_failure_livedump"></a>Bug 检查0x190： WIN32K.SYS \_ 严重 \_ 故障 \_ LIVEDUMP


WIN32K.SYS \_ 严重 \_ 故障 \_ LIVEDUMP bug 检查的值为0x00000190。 这表明 Win32k.sys 遇到了严重故障。 捕获实时转储以收集调试信息。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="win32k_critical_failure_livedump-parameters"></a>WIN32K.SYS \_ 严重 \_ 故障 \_ LIVEDUMP 参数


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
<td align="left"><p>失败类型</p>
<p>0x1： REGION_VALIDATION_FAILURE 区域超出了表面界限。</p>
2-指向 DC 3 的指针-指向 SURFACE 4 的指针-指向区域的指针
<p>0x2： OPERATOR_NEW_USED 运算符 "NEW" 用于分配内存。</p>
2-保留 3-保留 4-保留</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数1</td>
</tr>
</tbody>
</table>

 

 

 





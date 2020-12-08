---
title: 创建内核模式堆栈跟踪数据库
description: 创建内核模式堆栈跟踪数据库
keywords:
- " (全局标志创建内核模式堆栈跟踪数据库) "
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3be3fefaecfccd8808760055b3bb7563cb0de0fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841155"
---
# <a name="create-kernel-mode-stack-trace-database"></a>创建内核模式堆栈跟踪数据库


## <span id="ddk_create_kernel_mode_stack_trace_database_dtools"></span><span id="DDK_CREATE_KERNEL_MODE_STACK_TRACE_DATABASE_DTOOLS"></span>


" **创建内核模式堆栈跟踪数据库** " 标志创建核心操作（如资源对象和对象管理操作）的运行时堆栈跟踪数据库，并且仅在使用 Windows 的已检查内部版本时才有效。 在 Windows 10 版本1803之前，已检查的生成在 windows 的早期版本上可用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>kst</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x2000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_KERNEL_STACK_TRACE_DB</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

GFlags 将此标志显示为内核标志设置，但在运行时它是无效的，因为内核已经启动。

 

 






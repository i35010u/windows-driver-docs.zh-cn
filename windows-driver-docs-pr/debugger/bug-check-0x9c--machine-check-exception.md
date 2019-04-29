---
title: Bug 检查 0x9C MACHINE_CHECK_EXCEPTION
description: MACHINE_CHECK_EXCEPTION bug 检查具有 0x0000009C 值。 此 bug 检查指示发生致命计算机检查异常。
ms.assetid: b8945dba-c515-4a30-a36c-ef4feaadabbe
keywords:
- Bug 检查 0x9C MACHINE_CHECK_EXCEPTION
- MACHINE_CHECK_EXCEPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MACHINE_CHECK_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: abc5ee90d151b5c37dbc9d4053a4e92c105ef162
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324680"
---
# <a name="bug-check-0x9c-machinecheckexception"></a>Bug 检查 0x9C：机器\_检查\_异常


在计算机\_检查\_异常错误检查的值为 0x0000009C。 此 bug 检查指示发生致命计算机检查异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="machinecheckexception-parameters"></a>机器\_检查\_异常参数


消息中列出的四个参数具有不同的含义，具体取决于处理器的类型。

如果处理器上的较旧的基于 x86 的体系结构为基础，具有该计算机检查异常 (MCE) 功能，但不是计算机检查体系结构 (MCA) 功能 （例如，Intel Pentium 处理器），参数具有以下含义。

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
<td align="left"><p>低 32 位 P5_MC_TYPE 机服务报表 (MSR)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>MCA_EXCEPTION 结构的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>P5_MC_ADDR MSR 高 32 位</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>P5_MC_ADDR MSR 低 32 位</p></td>
</tr>
</tbody>
</table>

 

如果处理器上的较新的基于 x86 的体系结构为基础，具有 MCA 功能和 MCE 功能 （例如，任何的 6 个月或更高版本，如 Pentium Pro、 Pentium IV 或 Xeon 系列的 Intel 处理器），或者如果处理器是基于 x64 的处理器，参数都有以下几个含义。

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
<td align="left"><p>银行编号</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>MCA_EXCEPTION 结构的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>发生了错误 MCA bank MCi_STATUS MSR 高 32 位</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>发生了错误 MCA bank MCi_STATUS MSR 低 32 位</p></td>
</tr>
</tbody>
</table>

 

在基于 Itanium 处理器上，参数具有以下含义。

**请注意**  参数 1 指示冲突类型。

 

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>日志的地址</p></td>
<td align="left"><p>日志的大小</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>日志的地址</p></td>
<td align="left"><p>日志的大小</p></td>
<td align="left"><p>错误代码</p></td>
<td align="left"><p>系统抽象层 (SAL) 处理 MCA 时 SAL_GET_STATEINFO 返回了错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>日志的地址</p></td>
<td align="left"><p>日志的大小</p></td>
<td align="left"><p>错误代码</p></td>
<td align="left"><p>同时处理 MCA，SAL 为 SAL_CLEAR_STATEINFO 返回错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>日志的地址</p></td>
<td align="left"><p>日志的大小</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>固件 (FW) 报告严重 MCA。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>日志的地址</p></td>
<td align="left"><p>日志的大小</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>有两个可能的原因：</p>
<ul>
<li><p>SAL 报告可恢复 MCA，但当前不支持此恢复。</p></li>
<li><p>SAL 生成 MCA，但无法生成错误记录。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>日志的地址</p></td>
<td align="left"><p>日志的大小</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xC</p></td>
<td align="left"><p>日志的地址</p></td>
<td align="left"><p>日志的大小</p></td>
<td align="left"><p>错误代码</p></td>
<td align="left"><p>SAL 处理 INIT 事件时 SAL_GET_STATEINFO 返回了错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xD</p></td>
<td align="left"><p>日志的地址</p></td>
<td align="left"><p>日志的大小</p></td>
<td align="left"><p>错误代码</p></td>
<td align="left"><p>处理 INIT 事件时，SAL 为 SAL_CLEAR_STATEINFO 返回错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xE</p></td>
<td align="left"><p>日志的地址</p></td>
<td align="left"><p>日志的大小</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在 Windows Vista 和更高版本操作系统中，只有在以下情况下会执行此 bug 检查。

-   WHEA 未完全初始化。
-   Rendezvous 其寄存器中有任何错误的所有处理器。

对于其他情况下，此 bug 检查已替换为[ **bug 检查 0x124:WHEA\_无法纠正\_错误**](bug-check-0x124---whea-uncorrectable-error.md) Windows Vista 和更高版本操作系统中。

有关计算机检查体系结构 (MCA) 的详细信息，请参阅 Intel 或 AMD Web 站点。

 

 





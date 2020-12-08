---
title: Bug 检查 0x9C MACHINE_CHECK_EXCEPTION
description: MACHINE_CHECK_EXCEPTION bug 检查的值为0x0000009C。 此 bug 检查表明出现了严重计算机检查异常。
keywords:
- Bug 检查 0x9C MACHINE_CHECK_EXCEPTION
- MACHINE_CHECK_EXCEPTION
ms.date: 05/13/2020
topic_type:
- apiref
api_name:
- MACHINE_CHECK_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9bdff006fb1633ceaeef4ec50fb53e431e32de8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839327"
---
# <a name="bug-check-0x9c-machine_check_exception"></a>Bug 检查0x9C：计算机 \_ 检查 \_ 异常


计算机 \_ 检查 \_ 异常 bug 检查的值为0x0000009C。 此 bug 检查表明出现了严重计算机检查异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="machine_check_exception-parameters"></a>计算机 \_ 检查 \_ 异常参数


消息中列出的四个参数具有不同的含义，具体取决于处理器类型。

如果处理器基于较旧的基于 x86 的体系结构，并且具有计算机检查异常 (MCE) 功能，而不是计算机检查体系结构 (MCA) 功能 (例如，Intel Pentium 处理器) ，则这些参数具有以下含义。

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
<td align="left"><p>P5_MC_TYPE 机服务的低32位报告 (MSR) </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>MCA_EXCEPTION 结构的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>P5_MC_ADDR MSR 的高32位</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>P5_MC_ADDR MSR 的低32位</p></td>
</tr>
</tbody>
</table>

 

如果处理器基于较新的基于 x86 的体系结构，并且具有 MCA 功能和 MCE 功能 (例如，系列6或更高版本的任何 Intel 处理器，如 Pentium Pro、Pentium IV 或强) ，或者处理器是基于 x64 的处理器，则这些参数具有以下含义。

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
<td align="left"><p>出现错误的 MCA 银行 MCi_STATUS 的32位</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>出现错误的 MCA 银行 MCi_STATUS MSR 的低32位</p></td>
</tr>
</tbody>
</table>


<a name="remarks"></a>备注
-------

此 bug 检查仅在以下情况下发生。

-   WHEA 未完全初始化。
-   集合中的所有处理器在其寄存器中没有错误。

对于其他情况，此 bug 检查已替换为 bug 检查0x124： Windows Vista 和更高版本操作系统中的 [**WHEA 无法 \_ 纠正的 \_ 错误**](bug-check-0x124---whea-uncorrectable-error.md) 。

有关计算机检查体系结构 (MCA) 的详细信息，请参阅 Intel 或 AMD 网站。

 

 





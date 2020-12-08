---
title: 选择要删除的公共符号
description: 选择要删除的公共符号
keywords:
- Pdbcopy.exe，删除公共符号
- 符号，AgeStore
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fe7be9c81ebeb4a35d23f91e88fac309f4a39c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821603"
---
# <a name="choosing-which-public-symbols-to-remove"></a>选择要删除的公共符号


Pdbcopy.exe 提供了-f 和-F 选项，以便您可以从去除的符号文件中删除任意一组公共符号，只保留受众为了执行调试而需要访问的符号。

Pdbcopy.exe 的一个常见用途是创建一个特殊版本的符号文件，供 Microsoft 在其联机崩溃分析 (的 OCA) 计划中使用。 OCA 可以将某些函数指定为 *静态*，这意味着如果在堆栈跟踪中找到该函数，则将忽略该函数。 如果函数只是一个不执行重要计算的包装或 "传递" 函数，则通常会将该函数声明为静态。 如果在失败分析中的堆栈上发现此类函数，则假定此函数本身不是错误的，并且大多数情况下会将它传递到堆栈之前从例程收到的无效或损坏数据。 通过忽略此类函数，OCA 可以更好地确定错误或损坏的实际原因。

当然，要声明 "静态" 的任何函数都需要包含在 OCA 使用的符号文件的公共符号表中。 但是，这并不是需要包括的唯一函数，如下面的示例所示。

假设您编写了一个 Windows 驱动程序，并且使用 Pdbcopy.exe 从其符号文件中删除了所有公共符号（ **FunctionOne** 和 **FunctionSix** 除外），这两个静态函数除外。 您的期望是，如果在发生故障后在堆栈上找到 **FunctionOne** 或 **FunctionSix** ，则将忽略该故障。 如果驱动程序的任何其他部分位于堆栈上，Microsoft 将为你提供相应的内存地址，你可以使用该地址调试驱动程序。

不过，让我们假设你的驱动程序在以下布局中占用内存：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">地址</th>
<th align="left">内存内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>模块的基址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2000</p></td>
<td align="left"><p><strong>FunctionOne</strong>的开头</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x203F</p></td>
<td align="left"><p>结束 <strong>FunctionOne</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3000</p></td>
<td align="left"><p><strong>FunctionSix</strong>的开头</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x305F</p></td>
<td align="left"><p>结束 <strong>FunctionSix</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7FFF</p></td>
<td align="left"><p>内存中的模块结束</p></td>
</tr>
</tbody>
</table>

 

如果调试器查找堆栈上的地址，则会选择下一个较低地址的符号。 由于公共符号表包含每个符号的地址，但没有大小信息，因此调试器无法知道某个地址是否确实位于任何特定符号的边界内。

因此，如果地址0x2031 发生错误，则 Microsoft OCA 运行的调试器会正确地将错误标识为 **FunctionOne** 内的状态。 因为这是一个静态函数，所以调试器会继续遍历堆栈以找出崩溃的原因。

但是，如果0x2052 发生错误，则调试器仍会将此地址与 **FunctionOne** 匹配，即使它超出了此函数的实际结尾 (0x203F) 。

因此，您还必须在您的去除符号文件中包含您要公开的函数，还必须包含这些函数后面的符号。 在此示例中，你想要公开 **FunctionOne**、 **FunctionTwo**、 **FunctionSix** 和 **FunctionSeven**：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">地址</th>
<th align="left">内存内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>模块的基址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2000</p></td>
<td align="left"><p><strong>FunctionOne</strong>的开头</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x203F</p></td>
<td align="left"><p>结束 <strong>FunctionOne</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2040</p></td>
<td align="left"><p><strong>FunctionTwo</strong>的开头</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3000</p></td>
<td align="left"><p><strong>FunctionSix</strong>的开头</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x305F</p></td>
<td align="left"><p>结束 <strong>FunctionSix</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3060</p></td>
<td align="left"><p><strong>FunctionSeven</strong>的开头</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7FFF</p></td>
<td align="left"><p>内存中的模块结束</p></td>
</tr>
</tbody>
</table>

 

如果在去除的符号文件中包含所有这四个函数，则 Microsoft OCA 分析不会错误地将地址0x2052 视为 **FunctionOne** 的一部分。 在此示例中，它将假定此地址是 **FunctionTwo** 的一部分，但这并不重要，因为尚未将 **FunctionTwo** 注册为静态函数。 重要的是，地址0x2052 被识别为不落在静态函数内，因此，OCA 会将其识别为驱动程序内有意义的错误，并且可以通知您此错误。

如果你不希望在每个静态函数之后公布函数名称，则可以在每个静态函数后将不重要的函数插入到代码中，以便可以将这些函数的名称包含在公共符号文件中。 请确保在二进制文件的地址空间中，确保这些添加的函数确实沿用了静态函数，因为某些优化例程可能会改变这一点，甚至完全删除一些函数。

 

 






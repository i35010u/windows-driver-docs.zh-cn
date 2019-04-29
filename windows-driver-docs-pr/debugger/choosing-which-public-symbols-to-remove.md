---
title: 选择要删除的公共符号
description: 选择要删除的公共符号
ms.assetid: 0de89f65-ebb5-4186-a6f9-6676f86a75f1
keywords:
- PDBCopy，删除公共符号
- 符号 AgeStore
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1037cf0da20c92921234a65836c71b57a7c262db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375101"
---
# <a name="choosing-which-public-symbols-to-remove"></a>选择要删除的公共符号


PDBCopy 提供-f 和-F 选项，以便您可以保留你的受众需要访问，以便执行其调试这些符号从去除的符号文件，删除任意一组公共符号。

PDBCopy 的一个常见用途是在其在线崩溃分析 (OCA) 程序中创建以供 Microsoft 符号文件的特殊版本。 OCA 可以指定某些函数作为*静态*，这意味着，如果该函数位于堆栈上跟踪它将被忽略。 函数通常会声明静态如果只是包装器或"直通"函数的执行没有显著的计算。 如果故障分析在堆栈上找到此类函数，则可以此函数本身不是在发生故障，并且会最多传递无效或损坏的数据从例程在堆栈上前面收到的假定。 通过忽略此类函数，OCA 可以更好地确定错误或损坏的实际原因。

正常情况下，你想要"静态"声明任何函数需要包含 OCA 所使用的符号文件的公共符号表中。 但是，这些不是只需包含在内，如以下示例所示的函数。

假设您编写的 Windows 驱动程序和 PDBCopy 用于删除从其符号文件，所有公共符号除外**FunctionOne**并**FunctionSix**，两个静态函数。 你的预期是，如果任一**FunctionOne**或**FunctionSix**位于堆栈上崩溃后 OCA 将忽略它们。 如果您的驱动程序的任何其他部分在堆栈上，Microsoft 将向您提供相应的内存地址，并可以使用该地址来调试您的驱动程序。

但是，让我们假设您的驱动程序占用内存中的以下布局：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">地址</th>
<th align="left">内存中的内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>模块的基址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2000</p></td>
<td align="left"><p>开头<strong>FunctionOne</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x203F</p></td>
<td align="left"><p>结束的<strong>FunctionOne</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3000</p></td>
<td align="left"><p>开头<strong>FunctionSix</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x305F</p></td>
<td align="left"><p>结束的<strong>FunctionSix</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7FFF</p></td>
<td align="left"><p>在内存中模块的结尾</p></td>
</tr>
</tbody>
</table>

 

如果调试器在堆栈上找到一个地址，它将选择下一个较低地址的符号宽度。 由于公共符号表中包含的每个符号，但没有大小信息的地址，因此要知道是否地址实际上是任何特定符号的边界内的调试程序方法。

因此，如果出现故障，则在地址 0x2031，调试程序正常运行的 Microsoft OCA 标识将错误作为内位于**FunctionOne**。 由于这是一个静态函数，调试器会继续遍历堆栈以查找在发生崩溃的原因。

但是，如果错误发生在 0x2052，调试器仍会匹配到此地址**FunctionOne**，即使它位于实际 (0x203F) 此函数的末尾之外。

因此，您必须包括去除的符号文件中的函数希望公开，不仅还紧跟这些函数的符号。 在此示例中，你会想要公开**FunctionOne**， **FunctionTwo**， **FunctionSix**，以及**FunctionSeven**:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">地址</th>
<th align="left">内存中的内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>模块的基址</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2000</p></td>
<td align="left"><p>开头<strong>FunctionOne</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x203F</p></td>
<td align="left"><p>结束的<strong>FunctionOne</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2040</p></td>
<td align="left"><p>开头<strong>FunctionTwo</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3000</p></td>
<td align="left"><p>开头<strong>FunctionSix</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x305F</p></td>
<td align="left"><p>结束的<strong>FunctionSix</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3060</p></td>
<td align="left"><p>开头<strong>FunctionSeven</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7FFF</p></td>
<td align="left"><p>在内存中模块的结尾</p></td>
</tr>
</tbody>
</table>

 

如果在去除的符号文件中，包含这些函数的所有四个，则 Microsoft OCA 分析不会错误地将地址作为一部分 0x2052 **FunctionOne**。 在此示例中它将假定此地址是的一部分**FunctionTwo**，但该很不重要，因为你尚未注册**FunctionTwo**与 OCA 作为静态函数。 重要的一点是，地址 0x2052 识别为不属于静态函数和 OCA 因此会将此识别为您的驱动程序中的有意义错误并会告诉您该错误。

如果不希望 publicize 以下每个静态函数的函数的名称，可以将并不重要的函数插入到代码，以便可以在公共符号文件中包含这些函数的名称遵循每个静态函数。 请务必验证这些添加的函数由于一些优化例程可能会更改，或甚至完全删除某些功能确实会按照你的二进制文件的地址空间中静态函数。

 

 






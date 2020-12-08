---
title: 使用安全整数函数
description: Ntintsafe 库提供一组 C 函数，这些函数使用界限检查执行安全的整数算术运算，以防止内核模式代码中出现溢出和下溢。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 112b461c93479d3e27f9a0b746da1df4e2789437
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838453"
---
# <a name="using-safe-integer-functions"></a>使用安全整数函数


最大程度地减少安全问题的一种方法是防止整数溢出和下溢。 当算术运算的结果大于设置为接收数据类型的数据类型的内存空间时，将发生整数溢出。 这会导致截断整数和不正确的结果。 当操作（通常是减法）提供了不正确的结果时，将发生下溢。 两种数据类型之间的强制转换还会导致不能容纳新内存空间的结果截断导致错误的结果。

Ntintsafe 库提供一组 C 函数，这些函数使用界限检查执行安全的整数算术运算，以防止内核模式代码中出现溢出和下溢。 这些函数对应于应用程序代码使用的 Windows IntSafe 函数。 您可以使用这些函数来计算索引或缓冲区大小，或计算某种其他形式的边界检查。 函数针对速度进行了优化。

安全整数函数具有以下优势：

-   始终向函数提供目标缓冲区的大小，以确保函数不会写入缓冲区的末尾。
-   可以保证缓冲区以 null 结尾，即使操作截断了预期的结果。
-   所有函数都将返回 NTSTATUS，其中只有一个成功代码 (状态 \_ 成功) ，另一个可能的错误条件 (状态 \_ 整数 \_ 溢出) 。

Ntintsafe 库有两类函数：

-   **转换函数**-这些函数执行两种数据类型之间的转换。
-   **算术函数**-这些函数为每种数据类型执行加法、减法和乘法运算。 没有任何除法运算，因为没有溢出条件。

[内核模式安全整数函数摘要](summary-of-safe-integer-functions.md)

[导入内核模式安全整数函数](importing-safe-integer-functions.md)

 

 





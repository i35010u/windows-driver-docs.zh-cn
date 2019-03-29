---
title: 使用安全整数函数
description: Ntintsafe 库提供了一组边界检查以防止溢出和下的溢内核模式代码中执行安全整数算术运算的 C 函数。
ms.assetid: AFB7A078-814D-49EF-ABF9-2C621590F43B
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bf4674470dc58f8e75c0feeaeede0537080afbfe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577125"
---
# <a name="using-safe-integer-functions"></a>使用安全整数函数


最大程度减少安全问题的一种方法是为了防止整数溢出和下溢。 大于设置为接收它的数据类型的内存空间的算术运算的结果时，将发生整数溢出。 这会导致截断的整数部分和不正确的结果。 如果，发生下溢时的操作，通常减法，提供了不正确的结果。 两个数据之间强制转换类型也可能由于截断的结果，无法容纳新的内存空间而不正确的结果。

Ntintsafe 库提供了一组边界检查以防止溢出和下的溢内核模式代码中执行安全整数算术运算的 C 函数。 这些函数对应于由应用程序代码使用的 Windows IntSafe 函数。 若要计算索引或缓冲区的大小，或若要计算某种其他形式的边界检查，可使用这些函数。 针对速度进行了优化的函数。

安全整数函数具有以下优点：

-   目标缓冲区的大小始终提供到函数，以确保该函数不会写入超过缓冲区的末尾。
-   保证缓冲区以 null 结尾的即使该操作将截断想要的结果。
-   所有函数都返回 NTSTATUS，只有一个可能的成功代码 (状态\_成功) 和一个可能的错误条件 (状态\_整数\_溢出)。

Ntintsafe 库有两种类别的函数：

-   **转换函数**— 这些函数执行两个数据类型之间的转换。
-   **算术函数**— 这些函数执行加法、 减法、 和乘法运算的每种数据类型。 因为没有溢出条件，没有除法运算。

[内核模式安全整数函数的摘要](summary-of-safe-integer-functions.md)

[导入内核模式安全整数函数](importing-safe-integer-functions.md)

 

 





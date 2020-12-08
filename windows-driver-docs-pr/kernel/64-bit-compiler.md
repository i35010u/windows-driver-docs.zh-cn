---
title: 64 位编译器
description: 64 位编译器
keywords:
- 64位 WDK 内核，将驱动程序移植到
- 将驱动程序移植到64位 Windows
- 编译器 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a10f21a955008a7d136580b8c2cc8f70181d0e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820697"
---
# <a name="64-bit-compiler"></a>64 位编译器





转换32位驱动程序源代码以使用 [新的数据类型](the-new-data-types.md)后，可以使用64位编译器来识别最初丢失的与类型相关的任何问题。 首次为64位 Windows 编译此代码时，编译器可能会生成很多指针截断或类型不匹配警告。 使用这些警告作为指导使代码更可靠。 最好消除所有警告，尤其是指针截断警告。

下面是此类警告的一个示例：

```cpp
warning C4311: 'type cast' : pointer truncation from 'unsigned char *' to 'unsigned long '
```

例如，以下代码可生成 C4311 警告：

```cpp
buffer = (PUCHAR)srbControl;
(ULONG)buffer += srbControl->HeaderLength;
```

若要更正此代码，请进行以下更改：

```cpp
buffer = (PUCHAR)srbControl;
(ULONG_PTR)buffer += srbControl->HeaderLength;
```

### <a name="predefined-macros"></a>预定义宏

编译器定义以下宏来标识平台。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>宏</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>_WIN64</p></td>
<td><p>64位平台。</p></td>
</tr>
<tr class="even">
<td><p>_WIN32</p></td>
<td><p>32位平台。 此值还由64位编译器定义，以便向后兼容。</p></td>
</tr>
<tr class="odd">
<td><p>_WIN16</p></td>
<td><p>16位平台。</p></td>
</tr>
</tbody>
</table>

 

以下宏特定于体系结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>宏</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>_M_IA64</p></td>
<td><p>64位 Intel 平台。</p></td>
</tr>
<tr class="even">
<td><p>_M_IX86</p></td>
<td><p>32位 Intel 平台。</p></td>
</tr>
</tbody>
</table>

 

除了特定于体系结构的代码，请不要使用这些宏。 请尽可能使用 \_ WIN64、 \_ WIN32 和 \_ WIN16。

### <a name="64-bit-compiler-switches-and-warnings"></a>64位编译器开关和警告

可以使用警告选项来协助移植到64位 Windows。 -Wp64-W3 交换机启用以下警告：

-   **C4305**：截断警告。 例如，"return"：从 "无符号 int64" 截断为 "long"。

-   **C4311**：截断警告。 例如，"类型 cast"：从 "int \* \_ ptr64" 到 "int" 的指针截断。

-   **C4312**：转换为较大的警告。 例如，"类型 cast"：从 "int" 转换为 "int \* \_ ptr64" 的大小较大。

-   **C4318**：传递的长度为零。 例如，将常量零作为长度传递给 **memset** 函数。

-   **C4319**： Not 运算符。 例如，"~"：零将 "无符号长" 扩展到 \_ 更大的 "无符号 int64"。

-   **C4313**：调用具有冲突转换类型说明符和参数的 **printf** 系列函数。 例如，格式字符串中的 "printf"： "% p" 与 "int64" 类型的参数2冲突 \_ 。 另一个示例是调用 printf ( "% x"，指针 \_ 值) ; 这将导致截断上限32位。 正确的调用是 printf ( "% p"，指针 \_ 值) 。

-   **C4244**：与现有的警告 C4242 相同。 例如，"return"：从 " \_ int64" 转换为 "无符号整数" 可能会丢失数据。

 

 





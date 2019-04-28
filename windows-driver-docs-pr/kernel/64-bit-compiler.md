---
title: 64 位编译器
description: 64 位编译器
ms.assetid: c119d6b3-03e2-4ffc-b0a9-8077b141a2f1
keywords:
- 64 位 WDK 内核，移植到驱动程序
- 移植到 64 位 Windows 的驱动程序
- 编译器 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ddf89ab2851c8681f91e88c8a57c61ff4e23aa9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339210"
---
# <a name="64-bit-compiler"></a>64 位编译器





转换 32 位驱动程序源代码以使用后[新的数据类型](the-new-data-types.md)，可以使用 64 位编译器确定最初错过了任何类型相关的问题。 第一次将此代码编译为 64 位 Windows，编译器可能会生成多个指针截断或类型不匹配警告。 使用这些警告作为指南，以使代码更可靠。 它是很好的做法消除所有警告，尤其是指针截断警告。

以下是此类警告的示例：

```cpp
warning C4311: 'type cast' : pointer truncation from 'unsigned char *' to 'unsigned long '
```

例如，下面的代码可以生成 C4311 警告：

```cpp
buffer = (PUCHAR)srbControl;
(ULONG)buffer += srbControl->HeaderLength;
```

若要更正代码，进行以下更改：

```cpp
buffer = (PUCHAR)srbControl;
(ULONG_PTR)buffer += srbControl->HeaderLength;
```

### <a name="predefined-macros"></a>预定义的宏

编译器定义的以下宏来标识平台。

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
<td><p>在 64 位平台。</p></td>
</tr>
<tr class="even">
<td><p>_WIN32</p></td>
<td><p>在 32 位平台。 此外通过向后兼容性的 64 位编译器定义此值。</p></td>
</tr>
<tr class="odd">
<td><p>_WIN16</p></td>
<td><p>一个 16 位的平台。</p></td>
</tr>
</tbody>
</table>

 

下列宏是特定于体系结构。

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
<td><p>在 64 位 Intel 平台。</p></td>
</tr>
<tr class="even">
<td><p>_M_IX86</p></td>
<td><p>在 32 位 Intel 平台。</p></td>
</tr>
</tbody>
</table>

 

不要使用特定于体系结构的代码中使用这些宏除外。 请改用\_WIN64， \_WIN32，和\_WIN16 只要有可能。

### <a name="64-bit-compiler-switches-and-warnings"></a>64 位编译器开关和警告

没有警告选项，以帮助移植到 64 位 Windows。 -Wp64-W3 开关可以启用以下警告：

-   **C4305**:截断警告。 例如，"return": 从"unsigned 的 int64"到截断"long"。

-   **C4311**:截断警告。 例如，"类型强制转换": 从指针截断"int\*\_ptr64"为"整数"。

-   **C4312**:转换为更大大小警告。 例如，"类型强制转换": 从"int"为转换"int\*\_ptr64"更大。

-   **C4318**:传递长度为零。 例如，传递常量零作为到长度**优化了 memset**函数。

-   **C4319**:Not 运算符。 例如，"~": 零扩展"unsigned long"到"无符号\_int64"更大。

-   **C4313**:调用**printf**系列具有冲突的转换函数的类型说明符和自变量。 例如，"printf": 格式字符串中的"%p"冲突类型的参数 2"\_int64。" 另一个示例是调用 printf ("%x"中，指针\_值); 这将导致较高的 32 位被截断。 正确的调用是 printf ("%p"中，指针\_值)。

-   **C4244**:与现有的警告 C4242 相同。 例如，"return": 从转换"\_int64"到"unsigned int，"可能丢失数据。

 

 





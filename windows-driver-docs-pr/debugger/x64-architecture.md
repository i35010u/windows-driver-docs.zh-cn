---
title: x64 体系结构
description: x64 体系结构
ms.assetid: 6c0d92d5-cb16-4909-bae5-39fc5c15f736
keywords:
- x64 处理器，体系结构
- 寄存器中的，在 x64 处理器
- x64 处理器，注册
ms.date: 03/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: c0b3f92c2864a6d855d545934d7d35439d1653ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381912"
---
# <a name="x64-architecture"></a>x64 体系结构


## <span id="ddk_x64_architecture_dbg"></span><span id="DDK_X64_ARCHITECTURE_DBG"></span>


X64 体系结构是 x86 的向后兼容的扩展。 它提供旧的 32 位模式，这就相当于 x86，以及新的 64 位模式。

术语"x64"包括 AMD 64 和 Intel64。 指令集即将于完全相同。

### <a name="span-idregistersspanspan-idregistersspanspan-idregistersspanregisters"></a><span id="Registers"></span><span id="registers"></span><span id="REGISTERS"></span>注册

x64 扩展 x86 的 8 通用寄存器是 64 位，并添加 8 新的 64 位寄存器。 64 位寄存器具有名称，使用"r"，因此，例如 64 位扩展的起始**eax**称为**rax**。 命名新寄存器**r8**通过**r15**。

较低的 32 位、 16 位和每个寄存器的 8 位进行直接寻址操作数。 这包括寄存器，如**esi**，其低 8 位未以前寻址。 下表指定 64 位寄存器的下半部分的程序集语言的名称。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">64 位寄存器</th>
<th align="left">较低的 32 位</th>
<th align="left">低 16 位</th>
<th align="left">低 8 位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>rax</strong></p></td>
<td align="left"><p><strong>eax</strong></p></td>
<td align="left"><p><strong>ax</strong></p></td>
<td align="left"><p><strong>al</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>rbx</strong></p></td>
<td align="left"><p><strong>ebx</strong></p></td>
<td align="left"><p><strong>bx</strong></p></td>
<td align="left"><p><strong>bl</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>rcx</strong></p></td>
<td align="left"><p><strong>ecx</strong></p></td>
<td align="left"><p><strong>cx</strong></p></td>
<td align="left"><p><strong>cl</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>rdx</strong></p></td>
<td align="left"><p><strong>edx</strong></p></td>
<td align="left"><p><strong>dx</strong></p></td>
<td align="left"><p><strong>dl</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>rsi</strong></p></td>
<td align="left"><p><strong>esi</strong></p></td>
<td align="left"><p><strong>si</strong></p></td>
<td align="left"><p><strong>sil</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>rdi</strong></p></td>
<td align="left"><p><strong>edi</strong></p></td>
<td align="left"><p><strong>di</strong></p></td>
<td align="left"><p><strong>dil</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>rbp</strong></p></td>
<td align="left"><p><strong>ebp</strong></p></td>
<td align="left"><p><strong>bp</strong></p></td>
<td align="left"><p><strong>bpl</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>rsp</strong></p></td>
<td align="left"><p><strong>esp</strong></p></td>
<td align="left"><p><strong>sp</strong></p></td>
<td align="left"><p><strong>spl</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r8</strong></p></td>
<td align="left"><p><strong>r8d</strong></p></td>
<td align="left"><p><strong>r8w</strong></p></td>
<td align="left"><p><strong>r8b</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r9</strong></p></td>
<td align="left"><p><strong>r9d</strong></p></td>
<td align="left"><p><strong>r9w</strong></p></td>
<td align="left"><p><strong>r9b</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r10</strong></p></td>
<td align="left"><p><strong>r10d</strong></p></td>
<td align="left"><p><strong>r10w</strong></p></td>
<td align="left"><p><strong>r10b</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r11</strong></p></td>
<td align="left"><p><strong>r11d</strong></p></td>
<td align="left"><p><strong>r11w</strong></p></td>
<td align="left"><p><strong>r11b</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r12</strong></p></td>
<td align="left"><p><strong>r12d</strong></p></td>
<td align="left"><p><strong>r12w</strong></p></td>
<td align="left"><p><strong>r12b</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r13</strong></p></td>
<td align="left"><p><strong>r13d</strong></p></td>
<td align="left"><p><strong>r13w</strong></p></td>
<td align="left"><p><strong>r13b</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r14</strong></p></td>
<td align="left"><p><strong>r14d</strong></p></td>
<td align="left"><p><strong>r14w</strong></p></td>
<td align="left"><p><strong>r14b</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r15</strong></p></td>
<td align="left"><p><strong>r15d</strong></p></td>
<td align="left"><p><strong>r15w</strong></p></td>
<td align="left"><p><strong>r15b</strong></p></td>
</tr>
</tbody>
</table>

 

输出到 32 位 subregister 是自动零扩展到整个的 64 位寄存器的操作。 操作输出到 8 位或 16 位 subregisters*不*零扩展 (这是兼容的 x86 行为)。

高的 8 位**ax**， **bx**， **cx**，以及**dx**仍可访问作为**ah**， **bh**， **ch**， **dh**，但不能用于所有类型的操作数。

指令指针**eip**，并**标志**注册已扩展为 64 位 (**rip**并**rflags**分别) 也。

X64 处理器还提供了多个的浮点寄存器集：

-   8 个 80 位 x87 注册。

-   8 个 64 位 MMX 寄存器。 (这些与 x87 重叠注册。)

-   原始的一组 8 个 128 位 SSE 寄存器增加到十六个。

### <a name="span-idcallingconventionsspanspan-idcallingconventionsspanspan-idcallingconventionsspancalling-conventions"></a><span id="Calling_Conventions"></span><span id="calling_conventions"></span><span id="CALLING_CONVENTIONS"></span>调用约定

与不同的是 x86，C /C++编译器仅支持在 x64 上一个调用约定。 此调用约定在 x64 上充分利用可用的寄存器增加：

-   前四个整数或指针参数中传递**rcx**， **rdx**， **r8**，以及**r9**注册。

-   传递的前四个浮点参数中的前四个的 SSE 寄存器**xmm0**-**xmm3**。

-   调用方保留在寄存器中传递的参数在堆栈上的空间。 所调用的函数可以使用此空间溢出到堆栈寄存器的内容。

-   在堆栈上传递的任何其他参数。

-   中返回整数或指针的返回值**rax**注册，而在返回浮点值**xmm0**。

-   **到 rax**， **rcx**， **rdx**， **r8**-**r11**是易失性。

-   **rbx**， **rbp**， **rdi**， **rsi**， **r12**-**r15**将非易失性.

调用约定C++非常类似：**这**指针作为隐式的第一个参数传递。 接下来三个参数将传入寄存器，而其余部分传递到堆栈上。

### <a name="span-idaddressingmodesspanspan-idaddressingmodesspanspan-idaddressingmodesspanaddressing-modes"></a><span id="Addressing_Modes"></span><span id="addressing_modes"></span><span id="ADDRESSING_MODES"></span>寻址模式

在 64 位模式下的寻址模式是类似，但并不完全相同，x86。

- 64 位寄存器是指的说明将自动执行具有 64 位精度。 (例如**mov rax \[rbx\]** 移 8 个字节开始**rbx**到**rax**。)

- 一种特殊形式**mov**指令已添加了对 64 位即时常量或常量地址。 有关其他说明，即时常量或常量地址仍为 32 位。

- x64 提供了一个新**rip**-相对寻址模式。 引用单个常量地址的说明编码为从偏移量**rip**。 例如， **mov rax \[**  <em>addr</em> **\]** 指令将 8 个字节开始*addr*  + **rip**到**rax**。

说明，如**jmp**，**调用**，**推送**，以及**pop**的隐式引用指令指针和堆栈指针64 位 x64 上注册方式来处理它们。

 
## <a name="see-also"></a>请参阅

[X86-64 Wikipedia](https://en.wikipedia.org/wiki/X86-64)

[AMD 64 的开发人员资源](https://developer.amd.com/resources/)


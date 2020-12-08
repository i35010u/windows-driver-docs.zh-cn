---
title: x64 体系结构
description: x64 体系结构
keywords:
- x64 处理器，体系结构
- 在 x64 处理器上注册
- x64 处理器，寄存器
ms.date: 03/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8f4dc95e0b63eb3d776a19f622808a3f635e2eb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802721"
---
# <a name="x64-architecture"></a>x64 体系结构


## <span id="ddk_x64_architecture_dbg"></span><span id="DDK_X64_ARCHITECTURE_DBG"></span>


X64 体系结构是一个向后兼容的 x86 扩展。 它提供了与 x86 相同的旧式32位模式和新的64位模式。

术语 "x64" 包括 AMD 64 和 Intel64。 指令集接近相同。

### <a name="span-idregistersspanspan-idregistersspanspan-idregistersspanregisters"></a><span id="Registers"></span><span id="registers"></span><span id="REGISTERS"></span>寄存器

x64 将 x86's 8 通用寄存器扩展为64位，并添加8个新的64位寄存器。 64位寄存器的名称以 "r" 开头，例如， **eax** 的64位扩展称为 **rax**。 新寄存器通过 **r15** 名为 **r8** 。

每个寄存器的最低32位、16位和8位可直接在操作数中寻址。 这包括诸如 **esi** 的寄存器，此类 下表指定了64位寄存器下半部分的程序集语言名称。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">64位寄存器</th>
<th align="left">低32位</th>
<th align="left">低16位</th>
<th align="left">低8位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>rax</strong></p></td>
<td align="left"><p><strong>eax</strong></p></td>
<td align="left"><p><strong>ax</strong></p></td>
<td align="left"><p><strong>fc-al</strong></p></td>
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
<td align="left"><p><strong>磁盘</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>rsi</strong></p></td>
<td align="left"><p><strong>esi</strong></p></td>
<td align="left"><p><strong>si</strong></p></td>
<td align="left"><p><strong>sil</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>rdi.tpl</strong></p></td>
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
<td align="left"><p><strong>.rsp</strong></p></td>
<td align="left"><p><strong>能力</strong></p></td>
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

 

输出到32位 subregister 的操作会自动零扩展到整个64位寄存器。 输出到8位或16位 subregisters 的操作 *不* 会进行零扩展 (这是兼容的 x86 行为) 。

高8位的 **ax**、 **bx**、 **cx** 和 **dx** 仍可作为 **ah**、 **bh**、 **ch**、 **dh** 进行寻址，但不能与所有类型的操作数一起使用。

指令指针、 **eip** 和 **标志** 寄存器已扩展为64位 (**rip** 和) **rflags**。

X64 处理器还提供多组浮点寄存器：

-   8 80 位 x87 寄存器。

-   8 64 位 MMX 寄存器。  (这些与 x87 寄存器重叠。 ) 

-   原始的 8 128 位 SSE 寄存器集将增加到十六位。

### <a name="span-idcalling_conventionsspanspan-idcalling_conventionsspanspan-idcalling_conventionsspancalling-conventions"></a><span id="Calling_Conventions"></span><span id="calling_conventions"></span><span id="CALLING_CONVENTIONS"></span>调用约定

与 x86 不同，C/c + + 编译器仅支持 x64 上的一个调用约定。 此调用约定利用了 x64 上可用寄存器数量的增加：

-   在 **rcx**、 **rdx**、 **r8** 和 **r9** 寄存器中传递前四个整数或指针参数。

-   前四个浮点参数传递在前四个 SSE 寄存器 **xmm0** - **xmm3** 中。

-   调用方在堆栈上为注册中传递的参数保留空间。 被调用的函数可使用此空间将寄存器内容溢出到堆栈中。

-   任何其他参数将在堆栈上传递。

-   **Rax** 寄存器中返回一个整数或指针返回值，而浮点返回值则在 **xmm0** 中返回。

-   **rax**、 **rcx**、 **rdx**、 **r8** - **r11** 是可变的。

-   **rbx**、 **rbp**、 **rdi.tpl**、 **rsi**、 **r12** - **r15** 是非易失性。

C + + 调用约定非常类似： **此** 指针作为隐式第一个参数传递。 接下来的三个参数在寄存器中传递，而其余的参数在堆栈上传递。

### <a name="span-idaddressing_modesspanspan-idaddressing_modesspanspan-idaddressing_modesspanaddressing-modes"></a><span id="Addressing_Modes"></span><span id="addressing_modes"></span><span id="ADDRESSING_MODES"></span>寻址模式

64位模式下的寻址模式类似于 x86，但并不完全相同。

- 引用64位寄存器的指令自动以64位精度执行。  (例如 **mov rax， \[ rbx \]** 将8个字节从 **rbx** 开始移动到 **rax**。 ) 

- 添加了一种特殊形式的 **mov** 说明，适用于64位即时常量或常量地址。 对于所有其他说明，即时常量或常量地址仍然为32位。

- x64 提供了新的 **rip** 相对寻址模式。 引用单个常量地址的指令被编码为来自 **rip** 的偏移量。 例如， **mov rax， \[** <em>addr</em> **\]** 指令将从 *地址*  +  **rip** 开始到 **rax** 的8个字节。

**跳转**、 **call**、 **push** 和 **pop** 等说明隐式引用指令指针，堆栈指针将它们视为 x64 上的64位寄存器。

 
## <a name="see-also"></a>另请参阅

[X86-64 维基百科](https://en.wikipedia.org/wiki/X86-64)

[AMD 64 开发人员资源](https://developer.amd.com/resources/)


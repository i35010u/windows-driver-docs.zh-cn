---
title: 地址和地址范围语法
description: 地址和地址范围语法
ms.assetid: 3d4f41f1-07ec-484d-a748-27fbbb9bd0b2
ms.date: 07/24/2020
ms.localizationpriority: medium
ms.openlocfilehash: 65fa76dd1e92c8e508f2af6ea5694fad637b1e73
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264466"
---
# <a name="address-and-address-range-syntax"></a>地址和地址范围语法


## <span id="ddk_address_and_address_range_syntax_dbg"></span><span id="DDK_ADDRESS_AND_ADDRESS_RANGE_SYNTAX_DBG"></span>


在调试器中指定地址的方法有多种。

地址始终为*虚拟地址*，但文档特别指出了另一种类型的地址。 在用户模式下，调试器根据[当前进程](controlling-processes-and-threads.md)的页面目录解释虚拟地址。 在内核模式下，调试器根据[进程上下文](changing-contexts.md#process-context)指定的进程的页目录解释虚拟地址。 还可以直接设置*用户模式地址上下文*。 有关用户模式地址上下文的详细信息，请参阅[**context （设置用户模式地址上下文）**](-context--set-user-mode-address-context-.md)。

### <a name="span-idaddress_modes_and_segment_supportspanspan-idaddress_modes_and_segment_supportspanaddress-modes-and-segment-support"></a><span id="address_modes_and_segment_support"></span><span id="ADDRESS_MODES_AND_SEGMENT_SUPPORT"></span>地址模式和段支持

在基于 x86 的平台上，CDB 和 KD 支持以下寻址模式。 这些模式通过其前缀来区分。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">前缀</th>
<th align="left">名称</th>
<th align="left">地址类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%</p></td>
<td align="left"><p>公寓</p></td>
<td align="left"><p>32位地址（也是16位选择器，它指向32位段）和64位系统上的64位地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>&</p></td>
<td align="left"><p>虚拟86</p></td>
<td align="left"><p>实模式地址。 仅基于 x86。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#</p></td>
<td align="left"><p>plain</p></td>
<td align="left"><p>实模式地址。 仅基于 x86。</p></td>
</tr>
</tbody>
</table>

 

纯16位和虚拟86模式之间的区别在于，纯16位地址使用段值作为选择器并查找段说明符。 但虚拟86地址不使用选择器，而是直接映射到较低的 1 MB。

如果通过不是当前默认模式的寻址模式访问内存，则可以使用地址模式前缀来重写当前的地址模式。

### <a name="span-idaddress_argumentsspanspan-idaddress_argumentsspanaddress-arguments"></a><span id="address_arguments"></span><span id="ADDRESS_ARGUMENTS"></span>地址参数

Address 参数用于指定变量和函数的位置。 下表说明了可在 CDB 和 KD 中使用的各种地址的语法和含义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">语法</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>offset</p></td>
<td align="left"><p>虚拟内存空间中的绝对地址，具有对应于当前执行模式的类型。 例如，如果当前执行模式为16位，则偏移量为16位。 如果执行模式为32位，则偏移量为32位的偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>&</strong>[[segment：]] 偏移量</p></td>
<td align="left"><p>实际地址。 基于 x86 和基于 x64 的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>%</strong>段： [[offset]]</p></td>
<td align="left"><p>分段32位或64位地址。 基于 x86 和基于 x64 的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>%</strong>[[offset]]</p></td>
<td align="left"><p>虚拟内存空间中的绝对地址（32位或64位）。 基于 x86 和基于 x64 的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>名称 [[ <strong>+</strong> | <strong>−</strong> ]] 偏移量</p></td>
<td align="left"><p>平面32位或64位地址。 <em>name</em>可以是任何符号。 <em>offset</em>指定偏移量。 此偏移量可以是其前缀所指示的地址模式。 无前缀指定默认的模式地址。 您可以将偏移量指定为正（+）或负（−）值。</p></td>
</tr>
</tbody>
</table>

 

使用[**dg （显示选择器）**](dg--display-selector-.md)命令查看段描述符信息。

在 MASM 表达式中，还可以使用**poi**运算符来取消引用任何指针。 例如，如果地址0x00123456 处的指针指向 address location 0x00420000，则以下两个命令是等效的。

```dbgcmd
0:000> dd 420000 
0:000> dd poi(123456) 
```

在 c + + 表达式中，指针的行为类似于 c + + 中的指针。 但数字被解释为整数。 如果必须 deference 实际数字，则必须先对其进行转换，如下面的示例所示。

```dbgcmd
0:000> dd *( (long*) 0x123456 ) 
```

一些[伪寄存器](pseudo-register-syntax.md)还保存公用地址，如当前程序计数器位置。

还可以通过指定原始源文件名和行号来指示应用程序中的地址。 有关如何指定此信息的详细信息，请参阅[源行语法](source-line-syntax.md)。

### <a name="span-idaddress_rangesspanspan-idaddress_rangesspanaddress-ranges"></a><span id="address_ranges"></span><span id="ADDRESS_RANGES"></span>地址范围

可以通过一对地址或地址和对象计数来指定地址范围。

若要通过一对地址指定范围，请指定起始地址和结束地址。 例如，下面的示例是一个8字节的范围，从地址0x00001000 开始。

```dbgcmd
0x00001000  0x00001007
```

若要通过地址和对象计数指定地址范围，请指定 address 参数、字母 L （大写或小写）和值参数。 地址指定开始地址。 值指定要检查或显示的对象数。 对象的大小取决于命令。 例如，如果对象大小为1字节，则以下示例是从地址0x00001000 开始的8个字节的范围。

```dbgcmd
0x00001000  L8
```

但是，如果对象大小是一个双字（32位或4个字节），则以下两个范围分别给出8个字节的范围。

```dbgcmd
0x00001000  0x00001007
0x00001000  L2
```

还可以通过两种方法来指定值（**L * * * 大小*范围说明符）：

-   **L?** *大小*（带问号）表示与 **l * * 大小*相同，只是**l？** *Size*删除调试器的自动范围限制。 通常，范围限制为 256 MB，因为较大的范围是版式错误。 如果要指定大于 256 MB 的范围，则必须使用**L？** *大小*语法。

-   **L** *大小*（带有连字符）指定以给定地址结束的*长度范围*。 例如， **80000000 L20**指定从0X80000000 到0x8000001F 的范围， **80000000 L-20**指定从0x7FFFFFE0 到0x7fffffff 的范围。

要求地址范围的某些命令接受单个地址作为参数。 在这种情况下，该命令使用某些默认对象计数来计算范围的大小。 通常，地址范围为最后一个参数的命令将允许此语法。 有关每个命令的确切语法和默认范围大小，请参阅每个命令的参考主题。

## <a name="see-also"></a>另请参阅

若要显示有关内存的信息，请使用[！ address](-address.md)命令。 若要搜索内存，请使用[s （搜索内存）](s--search-memory-.md)命令。 若要显示内存的内容，请使用[d，da，db，dc，dd，dd，df，dp，dq，du，dw （显示内存）](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令。 有关如何使用内存窗口查看和编辑内存的信息，请参阅[使用内存窗口](memory-window.md)。

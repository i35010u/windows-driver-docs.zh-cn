---
title: 地址和地址范围语法
description: 地址和地址范围语法
ms.assetid: 3d4f41f1-07ec-484d-a748-27fbbb9bd0b2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c0854fe9a7abfdb574a2de3c04bbea3a70aaa69
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161413"
---
# <a name="address-and-address-range-syntax"></a>地址和地址范围语法


## <span id="ddk_address_and_address_range_syntax_dbg"></span><span id="DDK_ADDRESS_AND_ADDRESS_RANGE_SYNTAX_DBG"></span>


有几种方法在调试器中指定地址。

地址是始终*虚拟地址*，只是当文档专门指示另一个类型的地址。 在用户模式下，调试器将解释虚拟地址的页面目录根据[当前进程](controlling-processes-and-threads.md)。 在内核模式下，调试器将解释根据进程的页面目录的虚拟地址的[进程上下文](changing-contexts.md#process-context)指定。 您还可以直接设置*用户模式地址上下文*。 有关用户模式地址上下文的详细信息，请参阅[ **.context （设置用户模式地址上下文）** ](-context--set-user-mode-address-context-.md)。

### <a name="span-idaddress_modes_and_segment_supportspanspan-idaddress_modes_and_segment_supportspanaddress-modes-and-segment-support"></a><span id="address_modes_and_segment_support"></span><span id="ADDRESS_MODES_AND_SEGMENT_SUPPORT"></span>地址模式和线段支持

在基于 x86 的平台上 CDB 和 KD 支持以下寻址模式。 这些模式的区别的及其前缀。

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
<td align="left"><p>平面</p></td>
<td align="left"><p>32 位地址 （也 16 位选择器，指向 32 位段） 和 64 位系统上的 64 位地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>&</p></td>
<td align="left"><p>virtual 86</p></td>
<td align="left"><p>实模式地址。 基于 x86 的仅。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#</p></td>
<td align="left"><p>纯</p></td>
<td align="left"><p>实模式地址。 基于 x86 的仅。</p></td>
</tr>
</tbody>
</table>

 

普通和虚拟 86 模式之间的差异是一个普通的 16 位地址用作选择器使用的段值和查找的段描述符。 但虚拟 86 地址不使用选择器，而是映射直接到较低的 1 MB。

如果通过不是当前的默认模式的寻址模式访问内存，可以使用的地址模式前缀来重写当前的地址模式。

### <a name="span-idaddress_argumentsspanspan-idaddress_argumentsspanaddress-arguments"></a><span id="address_arguments"></span><span id="ADDRESS_ARGUMENTS"></span>地址参数

地址参数指定的变量和函数的位置。 下表说明的语法和可以在 CDB 和 KD 中使用的各种地址的含义。

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
<td align="left"><p>虚拟内存空间，含对应于当前的执行模式的类型中的绝对地址。 例如，如果当前的执行模式是 16 位，偏移量为 16 位。 如果执行模式是 32 位分段，偏移量为 32 位分段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>&</strong>[[段:]] 偏移量</p></td>
<td align="left"><p>实际地址。 基于 x86 和基于 x64 的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>%</strong>segment:[[ offset]]</p></td>
<td align="left"><p>分段的 32 位或 64 位地址。 基于 x86 和基于 x64 的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>%</strong>[[偏移量]]</p></td>
<td align="left"><p>一个绝对地址 （32 位或 64 位） 的虚拟内存空间中。 基于 x86 和基于 x64 的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>name[[ <strong>+</strong>|<strong>−</strong> ]] offset</p></td>
<td align="left"><p>一个平面 32 位或 64 位地址。 <em>名称</em>可以是任何符号。 <em>偏移量</em>指定的偏移量。 此偏移量可以是任何其前缀表示的地址模式。 无前缀指定默认模式地址。 您可以指定偏移量为正 （+） 或负值 （−）。</p></td>
</tr>
</tbody>
</table>

 

使用[ **dg （显示选择器）** ](dg--display-selector-.md)命令来查看段描述符信息。

在 MASM 表达式中，还可以使用**poi**运算符来取消任何指针。 例如，如果地址 0x00123456 处的指针指向地址位置 0x00420000，以下两个命令是等效的。

```dbgcmd
0:000> dd 420000 
0:000> dd poi(123456) 
```

在C++表达式，指针的行为方式类似于指针中C++。 但是，数字被解释为整数。 如果有 deference 实际数量，必须将其转换首先，如以下示例所示。

```dbgcmd
0:000> dd *( (long*) 0x123456 ) 
```

某些[伪寄存器](pseudo-register-syntax.md)还包含常用的地址，例如当前的程序计数器位置。

您还可以通过指定的原始源文件名和行号来指示应用程序中的地址。 有关如何指定此信息的详细信息，请参阅[源行语法](source-line-syntax.md)。

### <a name="span-idaddress_rangesspanspan-idaddress_rangesspanaddress-ranges"></a><span id="address_ranges"></span><span id="ADDRESS_RANGES"></span>地址范围

一对地址或地址和对象计数，可以指定的地址范围。

若要指定的范围由一对地址，指定的起始地址和结束地址。 例如，下面的示例是 8 个字节，从地址 0x00001000 开始的范围。

```dbgcmd
0x00001000  0x00001007
```

若要按地址和对象计数指定的地址范围，请指定地址参数、 字母 L （大写或小写） 和值参数。 地址指定的起始地址。 值指定要检查或显示的对象数。 对象的大小取决于该命令。 例如，如果对象大小为 1 个字节，下面的示例是 8 个字节，从地址 0x00001000 开始的范围。

```dbgcmd
0x00001000  L8
```

但是，如果对象大小为一个双字 （32 位或 4 个字节），以下两个范围每个为指定的 8 字节范围。

```dbgcmd
0x00001000  0x00001007
0x00001000  L2
```

有两种方法指定的值 (**L * * * 大小*范围说明符):

-   **L？** *大小*（其中将问号） 表示等同于 **L * * * 大小*，只不过**L？** *大小*删除了调试器的自动范围限制。 通常情况下，没有范围限制为 256 MB，因为更大范围是排字错误。 如果你想要指定大于 256 MB 的范围，则必须使用**L？** *大小*语法。

-   **L-** *大小*（以连字符） 指定的长度范围*大小*结束于给定的地址。 例如， **80000000 L20**指定的范围从 0x80000000 到 0x8000001F，并**80000000 L-20**指定范围内通过 0x7FFFFFFF 0x7FFFFFE0。

要求提供地址范围的一些命令作为参数接受一个地址。 在此情况下，该命令使用一些默认对象计数来计算的范围大小。 通常情况下，为其地址范围是最后一个参数的命令允许使用此语法。 确切语法和每个命令的默认范围大小，请参阅每个命令的参考主题。

 

 






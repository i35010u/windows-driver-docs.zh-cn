---
title: x86 指令
description: x86 指令
keywords:
- x86 处理器，说明
- x86 处理器，算术
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3eef0165bcd56c2d02ba55a2a070f6ac578bde0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802713"
---
# <a name="x86-instructions"></a>x86 指令


## <span id="ddk_x86_instructions_dbg"></span><span id="DDK_X86_INSTRUCTIONS_DBG"></span>


在此部分的列表中，用星号标记 ( * *\** _) 的说明尤其重要。 未标记的说明并不重要。

在 x86 处理器上，指令的大小是可变的，因此，向后反汇编是模式匹配中的练习。 若要从某一地址向后拆装，你应在以后开始反汇编，而不是真正想要转到的位置，然后继续进行，直到说明开始生效。 前几个说明可能并没有任何意义，因为你可能已在指令的中间开始反汇编。 遗憾的是，反汇编将永远不会与指令流同步，您必须在不同的起点尝试反汇编，直到找到起作用的起点。

对于打包好的 _ *switch** 语句，编译器会直接将数据发送到代码流中，因此通过 **switch** 语句进行的反汇编通常会碰到，因为它们实际上是数据) 的，因此不会有任何意义 (。 查找数据的末尾并继续反汇编。

### <a name="span-idinstruction_notationspanspan-idinstruction_notationspanspan-idinstruction_notationspaninstruction-notation"></a><span id="Instruction_Notation"></span><span id="instruction_notation"></span><span id="INSTRUCTION_NOTATION"></span>指令表示法

说明的一般表示法是将目标寄存器放在左侧，源位于右侧。 但是，此规则可能有一些例外情况。

通常，算术指令与源和目标寄存器组合在一起。 结果存储在目标中。

部分说明包含16位和32位版本，但此处仅列出了32位版本。 此处未列出的是浮点指令、特权指令和仅用于分段模型 (的指令，Microsoft Win32 不使用) 。

为了节省空间，许多指令以组合形式表示，如下面的示例中所示。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>  = <strong>r</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

表示第一个参数必须是寄存器，但第二个参数可以是寄存器、内存引用或直接值。

为了节省更多的空间，说明还可以表示，如下所示。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

这意味着第一个参数可以是寄存器或内存引用，第二个参数可以是寄存器、内存引用或即时值。

除非另有说明，否则在使用此缩写时，不能为源和目标选择内存。

而且，可以将位大小的后缀 (8，16，32) 可以追加到源或目标，以指示参数必须为该大小。 例如，r8 表示8位寄存器。

### <a name="span-idmemory__data_transfer__and_data_conversionspanspan-idmemory__data_transfer__and_data_conversionspanspan-idmemory__data_transfer__and_data_conversionspanmemory-data-transfer-and-data-conversion"></a><span id="Memory__Data_Transfer__and_Data_Conversion"></span><span id="memory__data_transfer__and_data_conversion"></span><span id="MEMORY__DATA_TRANSFER__AND_DATA_CONVERSION"></span>内存、数据传输和数据转换

内存和数据传输说明不会影响标志。

### <a name="span-ideffective_addressspanspan-ideffective_addressspanspan-ideffective_addressspaneffective-address"></a><span id="Effective_Address"></span><span id="effective_address"></span><span id="EFFECTIVE_ADDRESS"></span>有效地址

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>逆转</p></td>
<td align="left"><p><strong>r</strong>、m</p></td>
<td align="left"><p>加载有效地址。</p>
<p> (r = m) 的地址</p></td>
</tr>
</tbody>
</table>

 

例如，**逆转 eax， \[ esi + 4 \]** 表示 **eax**  =  **esi** + 4。 此指令通常用于执行算术运算。

### <a name="span-iddata_transferspanspan-iddata_transferspanspan-iddata_transferspandata-transfer"></a><span id="Data_Transfer"></span><span id="data_transfer"></span><span id="DATA_TRANSFER"></span>数据传输

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>MOV</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>MOVSX</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>移动到符号扩展。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>MOVZX</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>移动零扩展。</p></td>
</tr>
</tbody>
</table>

 

**MOVSX** 和 **MOVZX** 是对源到目标执行签名扩展或零扩展的 **mov** 指令的特殊版本。 这是允许源和目标不同大小的唯一说明。  (并且事实上，它们的大小必须不同。

### <a name="span-idstack_manipulationspanspan-idstack_manipulationspanspan-idstack_manipulationspanstack-manipulation"></a><span id="Stack_Manipulation"></span><span id="stack_manipulation"></span><span id="STACK_MANIPULATION"></span>堆栈操作

由 **esp** 寄存器指向堆栈。 位于 " **esp** " 的值是在最近推送 (堆栈的顶部) ;较旧的堆栈元素驻留在更高的地址上。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>推送</p></td>
<td align="left"><p><strong>r</strong>/m/#n</p></td>
<td align="left"><p>将值推送到堆栈上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>POP</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>堆栈中的 Pop 值。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>PUSHFD</p></td>
<td align="left"></td>
<td align="left"><p>将标志推送到堆栈上。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>POPFD</p></td>
<td align="left"></td>
<td align="left"><p>从堆栈中弹出标志。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>PUSHAD</p></td>
<td align="left"></td>
<td align="left"><p>推送所有整数寄存器。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>POPAD</p></td>
<td align="left"></td>
<td align="left"><p>弹出所有整数寄存器。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>Enter</p></td>
<td align="left"><p>#n，#n</p></td>
<td align="left"><p>生成堆栈帧。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>遗留</p></td>
<td align="left"></td>
<td align="left"><p>撕下堆栈帧</p></td>
</tr>
</tbody>
</table>

 

C/c + + 编译器不使用 **enter** 指令。  (**enter** 指令用于在 Algol 或 Pascal 等语言中实现嵌套过程 ) 

**Leave** 指令等效于：

```asm
mov esp, ebp
pop ebp
```

### <a name="span-iddata_conversionspanspan-iddata_conversionspanspan-iddata_conversionspandata-conversion"></a><span id="Data_Conversion"></span><span id="data_conversion"></span><span id="DATA_CONVERSION"></span>数据转换

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>CBW</p></td>
<td align="left"><p>将字节 (<strong>al</strong>) 转换为 word (<strong>ax</strong>) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CWD</p></td>
<td align="left"><p>将 word (<strong>ax</strong>) 转换为 dword (<strong>dx</strong>：<strong>ax</strong>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CWDE</p></td>
<td align="left"><p>将 word (<strong>ax</strong>) 转换为 dword (<strong>eax</strong>) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CDQ</p></td>
<td align="left"><p>将 dword (<strong>eax</strong>) 转换为 qword (<strong>edx</strong>：<strong>eax</strong>) 。</p></td>
</tr>
</tbody>
</table>

 

所有转换都执行符号扩展。

### <a name="span-idarithmetic_and_bit_manipulationspanspan-idarithmetic_and_bit_manipulationspanspan-idarithmetic_and_bit_manipulationspanarithmetic-and-bit-manipulation"></a><span id="Arithmetic_and_Bit_Manipulation"></span><span id="arithmetic_and_bit_manipulation"></span><span id="ARITHMETIC_AND_BIT_MANIPULATION"></span>算术和位操作

所有算术和位操作指令修改标志。

### <a name="span-idarithmeticspanspan-idarithmeticspanspan-idarithmeticspanarithmetic"></a><span id="Arithmetic"></span><span id="arithmetic"></span><span id="ARITHMETIC"></span>算术

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>ADD</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m + = <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>ADC</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m + = <strong>r2</strong>/m/#n + 执行</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>子项</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m-= <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>SBB</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m-= <strong>r2</strong>/m/#n + 执行</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>负面</p></td>
<td align="left"><p><strong>r1</strong>/m</p></td>
<td align="left"><p><strong>r1</strong>/m =-<strong>r1</strong>/m</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>增量</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p><strong>r</strong>/m + = 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>DEC</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p><strong>r</strong>/m-= 1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>CMP</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p>计算 <strong>r1</strong>/m- <strong>r2</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

**Cmp** 指令计算减法，并根据结果设置标志，但会引发结果。 它通常后跟一个测试减法结果的条件 **跳转** 指令。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>MUL</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p><strong>ax</strong>  = <strong>al</strong> * <strong>r</strong>/m8</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>MUL</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p><strong>dx</strong>：<strong>ax</strong>  =  <strong>ax</strong> * <strong>r</strong>/m16</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>MUL</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p><strong>edx</strong>：<strong>eax</strong>  =  <strong>eax</strong> * <strong>r</strong>/m32</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p><strong>ax</strong>  = <strong>al</strong> * <strong>r</strong>/m8</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p><strong>dx</strong>：<strong>ax</strong>  =  <strong>ax</strong> * <strong>r</strong>/m16</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p><strong>edx</strong>：<strong>eax</strong>  =  <strong>eax</strong> * <strong>r</strong>/m32</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/m</p></td>
<td align="left"><p><strong>r1</strong>  *= <strong>r2</strong>/m</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/m #n</p></td>
<td align="left"><p><strong>r1</strong>  = <strong>r2</strong>/m * #n</p></td>
</tr>
</tbody>
</table>

 

无符号和符号的乘法。 乘法后标志的状态未定义。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>V</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p> (<strong>ah</strong>， <strong>al</strong>) = (<strong>ax</strong>  %  <strong>r</strong>/m8， <strong>ax</strong>  /  <strong>r</strong>/m8) </p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>V</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p> (<strong>dx</strong>， <strong>ax</strong>) = <strong>dx</strong>：<strong>ax</strong>  /  <strong>r</strong>/m16</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>V</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p> (<strong>edx</strong>， <strong>eax</strong>) = <strong>edx</strong>：<strong>eax</strong>  /  <strong>r</strong>/m32</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>IDIV</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p> (<strong>ah</strong>， <strong>al</strong>) = <strong>ax</strong>  /  <strong>r</strong>/m8</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>IDIV</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p> (<strong>dx</strong>， <strong>ax</strong>) = <strong>dx</strong>：<strong>ax</strong>  /  <strong>r</strong>/m16</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IDIV</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p> (<strong>edx</strong>， <strong>eax</strong>) = <strong>edx</strong>：<strong>eax</strong>  /  <strong>r</strong>/m32</p></td>
</tr>
</tbody>
</table>

 

无符号和有符号分割。 伪代码说明中的第一个寄存器会接收余数，第二个寄存器接收商。 如果结果溢出了目标，则会生成除法溢出异常。

除法后标志的状态为 undefined。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>*</p></td>
<td align="left"><p>设置<em>cc</em></p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p>将 <strong>r</strong>/m8 设置为0或1</p></td>
</tr>
</tbody>
</table>

 

如果条件 *cc* 为 true，则8位值设置为1。 否则，8位值将设置为零。

### <a name="span-idbinary-coded_decimalspanspan-idbinary-coded_decimalspanspan-idbinary-coded_decimalspanbinary-coded-decimal"></a><span id="Binary-coded_Decimal"></span><span id="binary-coded_decimal"></span><span id="BINARY-CODED_DECIMAL"></span>二进制编码的十进制

除非调试用 COBOL 编写的代码，否则不会看到这些说明。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>DAA</p></td>
<td align="left"><p>加法后进行小数点调整。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>转移</p></td>
<td align="left"><p>在减法后调整小数。</p></td>
</tr>
</tbody>
</table>

 

这些说明在执行打包的二进制编码的十进制运算后调整 **al** 寄存器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>AAA</p></td>
<td align="left"><p>添加 ASCII 后进行调整。</p></td>
</tr>
<tr class="even">
<td align="left"><p>.AAS</p></td>
<td align="left"><p>在减法后调整 ASCII。</p></td>
</tr>
</tbody>
</table>

 

这些说明在执行解压缩的二进制编码的十进制运算后调整 **al** 寄存器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>AAM</p></td>
<td align="left"><p>乘法后的 ASCII 调整。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AAD</p></td>
<td align="left"><p>划分后的 ASCII 调整。</p></td>
</tr>
</tbody>
</table>

 

这些说明将在执行解压缩的二进制编码的十进制运算后调整 **al** 和 **ah** 寄存器。

### <a name="span-idbitsspanspan-idbitsspanspan-idbitsspanbits"></a><span id="Bits"></span><span id="bits"></span><span id="BITS"></span>带宽

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>AND</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m 和 <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>OR</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m 或 <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>XOR</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m xor <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>NOT</p></td>
<td align="left"><p><strong>r1</strong>/m</p></td>
<td align="left"><p><strong>r1</strong>/m = 位非 <strong>r1</strong>/m</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>TEST</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>r2</strong>/m/#n</p></td>
<td align="left"><p>计算 <strong>r1</strong>/m 和 <strong>r2</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

**测试** 指令计算逻辑 "与" 运算符，并根据结果设置标志，但会引发结果。 它通常后跟一个测试逻辑 AND 的结果的条件跳转指令。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>SHL</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &lt; &lt; =  <strong>cl</strong>/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>SHR</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &gt; &gt; =  <strong>cl</strong>/#n 零填充</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>SAR</p></td>
<td align="left"><p><strong>r1</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &gt; &gt; =  <strong>cl</strong>/#n 符号-填充</p></td>
</tr>
</tbody>
</table>

 

上移出的最后一个位将放置在 "执行" 中。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>SHLD</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>左移一倍。</p></td>
</tr>
</tbody>
</table>

 

按 **cl** n 向左移动 **r1** / \# ，用 **r2**/m。的顶层填充 上移出的最后一个位将放置在 "执行" 中。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>SHRD</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/m、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>右移 double。</p></td>
</tr>
</tbody>
</table>

 

按 **cl** n 向下移位 **r1** / \# ，用 **r2**/m。的下半位数填充 上移出的最后一个位将放置在 "执行" 中。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>角色</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>按<strong>cl</strong>/#n 向左旋转<strong>r1</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ROR</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>按<strong>cl</strong>/#n 将<strong>r1</strong>向右旋转。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RCL</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>按<strong>cl</strong>/#n 向左旋转<strong>r1</strong>/c。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RCR</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>cl</strong>/#n</p></td>
<td align="left"><p>按<strong>cl</strong>/#n 向右旋转<strong>r1</strong>/c。</p></td>
</tr>
</tbody>
</table>

 

旋转类似于移位，只不过移出的位将重新出现为传入的填充位。 旋转指令的 C 语言版本将携带位合并到旋转中。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>BT</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/#n</p></td>
<td align="left"><p>将<strong>r1</strong>的位<strong>r2</strong>/#n 复制到 "" 中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BTS</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/#n</p></td>
<td align="left"><p>设置<strong>r1</strong>的位<strong>r2</strong>/#n，将上一个值复制到 "中"。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BTC</p></td>
<td align="left"><p><strong>r1</strong>、 <strong>r2</strong>/#n</p></td>
<td align="left"><p>清除 " <strong>r1</strong> <strong>r2</strong>/#n"，将上一个值复制到 "携带"。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcontrol_flowspanspan-idcontrol_flowspanspan-idcontrol_flowspancontrol-flow"></a><span id="Control_Flow"></span><span id="control_flow"></span><span id="CONTROL_FLOW"></span>控制流

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>J<em>cc</em></p></td>
<td align="left"><p>目的</p></td>
<td align="left"><p>Branch 条件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>跳转</p></td>
<td align="left"><p>目的</p></td>
<td align="left"><p>直接跳转。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>跳转</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>间接跳过。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>CALL</p></td>
<td align="left"><p>目的</p></td>
<td align="left"><p>直接调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>CALL</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>间接调用。</p></td>
</tr>
</tbody>
</table>

 

**Call** 指令将返回地址推送到堆栈上，然后跳转到目标。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>RET</p></td>
<td align="left"><p><em>#北</em></p></td>
<td align="left"><p>返回</p></td>
</tr>
</tbody>
</table>

 

**Ret** 指令将会弹出，并跳到堆栈上的返回地址。 **RET** 指令中的非零 *\# n* 指示在弹出返回地址后，应将值 *\# n* 添加到堆栈指针。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>圈</p></td>
<td align="left"><p>如果结果为非零，则递减 <strong>ecx</strong> 并跳转。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LOOPZ</p></td>
<td align="left"><p>如果结果为非零且设置了<strong>zr</strong> ，则递减<strong>ecx</strong>和跳出。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LOOPNZ</p></td>
<td align="left"><p>如果结果为非零值，则递减 <strong>ecx</strong> ，跳转，并清除 <strong>zr</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>JECXZ</p></td>
<td align="left"><p>当 <strong>ecx</strong> 为零时跳转。</p></td>
</tr>
</tbody>
</table>

 

这些说明是 x86's CISC 遗产的残留项，在最近的处理器中，其速度远低于以较长的方式编写的等效说明。

### <a name="span-idstring_manipulationspanspan-idstring_manipulationspanspan-idstring_manipulationspanstring-manipulation"></a><span id="String_Manipulation"></span><span id="string_manipulation"></span><span id="STRING_MANIPULATION"></span>字符串操作

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>MOVS<em>T</em></p></td>
<td align="left"><p>将 <em>T</em> 从 <strong>esi</strong> 移到 <strong>edi。</strong></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>CMPS<em>T</em></p></td>
<td align="left"><p>将来自<strong>esi</strong>的<em>T</em>与 edi 进行比较<strong>。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>SCAS<em>T</em></p></td>
<td align="left"><p>Acc <em>T</em> t 的<strong>edi</strong>扫描<em>。</em></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>LODS<em>T</em></p></td>
<td align="left"><p>从<strong>esi</strong>将<em>t</em>加载到 acc<em>T 中。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>STOS<em>T</em></p></td>
<td align="left"><p>从 acc t 将 <em>t</em> 存储到 <strong>edi</strong> <em>。</em></p></td>
</tr>
</tbody>
</table>

 

执行该操作后，根据方向标志的设置 (向上或向下) ，sizeof (*T*) 会递增或递减源寄存器和目标寄存器。

指令可以作为 " **代表** " 的前缀，以将操作重复由 **ecx** register 指定的次数。

使用 **代表 mov** 指令来复制内存块。

**Rep stos** 指令用于使用 acc *T* 填充内存块。

### <a name="span-idflagsspanspan-idflagsspanspan-idflagsspanflags"></a><span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>随意

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>LAHF</p></td>
<td align="left"><p>从标志加载 <strong>ah</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SAHF</p></td>
<td align="left"><p>将 <strong>ah</strong> 存储到标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STC</p></td>
<td align="left"><p>设置 "执行"。</p></td>
</tr>
<tr class="even">
<td align="left"><p>简称</p></td>
<td align="left"><p>清除 "执行"。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CMC</p></td>
<td align="left"><p>求补。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STD</p></td>
<td align="left"><p>将方向设置为 <em>向下。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLD</p></td>
<td align="left"><p>将方向设置为 <em>向上。</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>STI</p></td>
<td align="left"><p>启用中断。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLI</p></td>
<td align="left"><p>禁用中断。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinterlocked_instructionsspanspan-idinterlocked_instructionsspanspan-idinterlocked_instructionsspaninterlocked-instructions"></a><span id="Interlocked_Instructions"></span><span id="interlocked_instructions"></span><span id="INTERLOCKED_INSTRUCTIONS"></span>联锁说明

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>XCHG</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>交换 <strong>r1</strong> 和 <strong>r</strong>/m。</p></td>
</tr>
<tr class="even">
<td align="left"><p>XADD</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>将 <strong>r1</strong> 添加到 <strong>r</strong>/m，并将原始值放入 <strong>r1。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CMPXCHG</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>比较和交换条件。</p></td>
</tr>
</tbody>
</table>

 

**Cmpxchg** 指令是以下的原子版本：

```asm
   cmp     accT, r/m
   jz      match
   mov     accT, r/m
   jmp     done
match:
   mov     r/m, r1
done:
```

### <a name="span-idmiscellaneousspanspan-idmiscellaneousspanspan-idmiscellaneousspanmiscellaneous"></a><span id="Miscellaneous"></span><span id="miscellaneous"></span><span id="MISCELLANEOUS"></span>杂

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>INT</p></td>
<td align="left"><p>#n</p></td>
<td align="left"><p>捕获到内核。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>绑定</p></td>
<td align="left"><p><strong>r</strong>、m</p></td>
<td align="left"><p>如果 <strong>r</strong> 不在范围内，则陷阱。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>NOP</p></td>
<td align="left"></td>
<td align="left"><p>无操作。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>XLATB</p></td>
<td align="left"></td>
<td align="left"><p><strong>al</strong> = [<strong>ebx</strong> + <strong>al</strong>]</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>BSWAP</p></td>
<td align="left"><p><strong>r</strong></p></td>
<td align="left"><p>在 register 中交换字节顺序。</p></td>
</tr>
</tbody>
</table>

 

下面是 **int** 指令的特例。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>INT</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>调试器断点捕获。</p></td>
</tr>
</tbody>
</table>

 

**INT 3** 的操作码为0xCC。 **NOP** 的操作码为0x90。

调试代码时，可能需要修补某些代码。 为此，可以将有问题的字节替换为0x90。

### <a name="span-ididiomsspanspan-ididiomsspanspan-ididiomsspanidioms"></a><span id="Idioms"></span><span id="idioms"></span><span id="IDIOMS"></span>惯例

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>XOR</p></td>
<td align="left"><p><strong>r</strong>、 <strong>r</strong></p></td>
<td align="left"><p><strong>r</strong> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>TEST</p></td>
<td align="left"><p><strong>r</strong>、 <strong>r</strong></p></td>
<td align="left"><p>检查 <strong>r</strong> = 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>ADD</p></td>
<td align="left"><p><strong>r</strong>、 <strong>r</strong></p></td>
<td align="left"><p>将 <strong>r</strong> 向左移动1。</p></td>
</tr>
</tbody>
</table>

 

 

 






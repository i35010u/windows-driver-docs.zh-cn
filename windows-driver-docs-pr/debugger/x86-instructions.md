---
title: x86 指令
description: x86 指令
ms.assetid: 237796d5-ef82-4eab-8d56-3191b3e63597
keywords:
- x86 处理器，说明
- x86 处理器，算术
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2310fd4e39c0c1072df7099c58c35bdc808cf2be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381897"
---
# <a name="x86-instructions"></a>x86 指令


## <span id="ddk_x86_instructions_dbg"></span><span id="DDK_X86_INSTRUCTIONS_DBG"></span>


在本部分中的列表，说明标有星号 (* *\\* * *) 尤为重要。 说明不因此标记为不重要。

X86 处理器，说明是可变的因此拆装向后是一个在模式匹配中的过程。 若要拆装发件人地址的向后，应启动拆装点进一步返回比真正想要转，并期待直到说明开始十分有意义。 第一个几条指令可能未利用任何有意义，因为您可能已启动反汇编指令的中间。 没有一种可能，遗憾的是，反汇编将永远不会将与指令流同步，您将必须尝试拆装，在不同的起始点，直到找到适用的起始点。

有关格式打包**切换**语句，则编译器将发出数据直接到代码流中，因此通过拆装**切换**语句将通常找进行任何有意义 （的说明因为它们是真正的数据）。 查找数据的末尾，并存在继续拆装。

### <a name="span-idinstructionnotationspanspan-idinstructionnotationspanspan-idinstructionnotationspaninstruction-notation"></a><span id="Instruction_Notation"></span><span id="instruction_notation"></span><span id="INSTRUCTION_NOTATION"></span>指令表示法

有关说明常规的表示法是放入目标寄存器左侧和右侧的源。 但是，可以是此规则的一些例外情况。

算术说明分别通常两个注册的源和目标寄存器组合。 将结果存储到目标。

某些指令具有 16 位和 32 位版本，但此处列出了仅 32 位版本。 不在下面列出了浮点指令、 特权的指令和使用仅在分段模型 （这可不使用 Microsoft Win32） 中的说明。

为节省空间，许多说明表示形式的组合，如下面的示例中所示。

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
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong> = <strong>r</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

表示第一个参数必须是寄存器中，但第二个可以是寄存器、 内存的参考信息或即时值。

若要保存更多的空间，说明还可以表示为如下所示。

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
<td align="left"><p><strong>r1</strong>/m， <strong>r</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r</strong>/m/#n</p></td>
</tr>
</tbody>
</table>

 

这意味着第一个参数可以是寄存器或内存的引用，第二个可以注册、 内存引用或即时值。

除非另行说明，使用此缩写词时，不能选择内存可用于源和目标。

此外，位大小后缀 （8、 16、 32） 可以追加到源或目标，以指示该参数必须是该大小。 例如，r8 表示一个 8 位寄存器。

### <a name="span-idmemorydatatransferanddataconversionspanspan-idmemorydatatransferanddataconversionspanspan-idmemorydatatransferanddataconversionspanmemory-data-transfer-and-data-conversion"></a><span id="Memory__Data_Transfer__and_Data_Conversion"></span><span id="memory__data_transfer__and_data_conversion"></span><span id="MEMORY__DATA_TRANSFER__AND_DATA_CONVERSION"></span>内存、 数据传输和数据转换

内存和数据传输指令不影响标志。

### <a name="span-ideffectiveaddressspanspan-ideffectiveaddressspanspan-ideffectiveaddressspaneffective-address"></a><span id="Effective_Address"></span><span id="effective_address"></span><span id="EFFECTIVE_ADDRESS"></span>有效地址

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
<td align="left"><p>LEA</p></td>
<td align="left"><p><strong>r</strong>，m</p></td>
<td align="left"><p>加载有效地址。</p>
<p>(r = m 的地址)</p></td>
</tr>
</tbody>
</table>

 

例如，**逆转 eax \[esi + 4\]** 意味着**eax** = **esi** + 4。 此指令通常用于执行算术运算。

### <a name="span-iddatatransferspanspan-iddatatransferspanspan-iddatatransferspandata-transfer"></a><span id="Data_Transfer"></span><span id="data_transfer"></span><span id="DATA_TRANSFER"></span>数据传输

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
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>MOVSX</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>移动使用符号扩展。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>MOVZX</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>移动通过零扩展。</p></td>
</tr>
</tbody>
</table>

 

**MOVSX**并**MOVZX**特殊版本的**mov**从源到目标执行符号扩展或零个扩展的指令。 这是唯一允许的源和目标为不同大小的说明。 （并且实际上，它们必须是不同的大小。

### <a name="span-idstackmanipulationspanspan-idstackmanipulationspanspan-idstackmanipulationspanstack-manipulation"></a><span id="Stack_Manipulation"></span><span id="stack_manipulation"></span><span id="STACK_MANIPULATION"></span>堆栈操作

指向堆栈**esp**注册。 处的值**esp**是 （最近推入堆栈，首先弹出）; 堆栈顶部的较旧堆栈元素驻留在较高的地址。

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
<td align="left"><p>推送到堆栈上的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>POP</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>将值从堆栈中弹出。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>PUSHFD</p></td>
<td align="left"></td>
<td align="left"><p>推送到堆栈上的标志。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>POPFD</p></td>
<td align="left"></td>
<td align="left"><p>弹出堆栈中的标志。</p></td>
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
<td align="left"><p>进入</p></td>
<td align="left"><p>#n，#n</p></td>
<td align="left"><p>生成堆栈帧。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>将保留</p></td>
<td align="left"></td>
<td align="left"><p>关闭堆栈帧</p></td>
</tr>
</tbody>
</table>

 

C /C++编译器不使用**输入**指令。 (**输入**指令用于在 Algol 或 Pascal 等语言中实现嵌套的过程。)

**离开**指令是等效于：

```asm
mov esp, ebp
pop ebp
```

### <a name="span-iddataconversionspanspan-iddataconversionspanspan-iddataconversionspandata-conversion"></a><span id="Data_Conversion"></span><span id="data_conversion"></span><span id="DATA_CONVERSION"></span>数据转换

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>CBW</p></td>
<td align="left"><p>转换字节 (<strong>al</strong>) 到 word (<strong>ax</strong>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CWD</p></td>
<td align="left"><p>转换单词 (<strong>ax</strong>) 为 dword (<strong>dx</strong>:<strong>ax</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CWDE</p></td>
<td align="left"><p>转换单词 (<strong>ax</strong>) 为 dword (<strong>eax</strong>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CDQ</p></td>
<td align="left"><p>转换 dword (<strong>eax</strong>) 到 qword (<strong>edx</strong>:<strong>eax</strong>)。</p></td>
</tr>
</tbody>
</table>

 

所有转换都执行符号扩展。

### <a name="span-idarithmeticandbitmanipulationspanspan-idarithmeticandbitmanipulationspanspan-idarithmeticandbitmanipulationspanarithmetic-and-bit-manipulation"></a><span id="Arithmetic_and_Bit_Manipulation"></span><span id="arithmetic_and_bit_manipulation"></span><span id="ARITHMETIC_AND_BIT_MANIPULATION"></span>算术运算符和位操作

所有算术和位操作说明修改标志。

### <a name="span-idarithmeticspanspan-idarithmeticspanspan-idarithmeticspanarithmetic"></a><span id="Arithmetic"></span><span id="arithmetic"></span><span id="ARITHMETIC"></span>算术运算

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
<td align="left"><p>添加</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong>/m + = <strong>r2</strong>/m/ #n</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>ADC</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong>/m + = <strong>r2</strong>/m/ #n + 携带</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>SUB</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong>/m -= <strong>r2</strong>/m/#n</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>SBB</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong>/m -= <strong>r2</strong>/m/#n + carry</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>NEG</p></td>
<td align="left"><p><strong>r1</strong>/m</p></td>
<td align="left"><p><strong>r1</strong>/m = -<strong>r1</strong>/m</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>INC</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p><strong>r</strong>/m + = 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>年 12 月</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p><strong>r</strong>/m -= 1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>CMP</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p>计算<strong>r1</strong>/m- <strong>r2</strong>/m/ #n</p></td>
</tr>
</tbody>
</table>

 

**Cmp**指令计算该减法运算和设置标志根据结果，但会抛弃结果。 通常跟条件**跳转**指令，用于测试该减法运算的结果。

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
<td align="left"><p><strong>ax</strong> = <strong>al</strong> * <strong>r</strong>/m8</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>MUL</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p><strong>dx</strong>:<strong>ax</strong> = <strong>ax</strong> * <strong>r</strong>/m16</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>MUL</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p><strong>edx</strong>:<strong>eax</strong> = <strong>eax</strong> * <strong>r</strong>/m32</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p><strong>ax</strong> = <strong>al</strong> * <strong>r</strong>/m8</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p><strong>dx</strong>:<strong>ax</strong> = <strong>ax</strong> * <strong>r</strong>/m16</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p><strong>edx</strong>:<strong>eax</strong> = <strong>eax</strong> * <strong>r</strong>/m32</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r2</strong>/m</p></td>
<td align="left"><p><strong>r1</strong> *= <strong>r2</strong>/m</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IMUL</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r2</strong>/m、 #n</p></td>
<td align="left"><p><strong>r1</strong> = <strong>r2</strong>/m * #n</p></td>
</tr>
</tbody>
</table>

 

未签名和签名乘法。 标志后乘法是不确定状态。

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
<td align="left"><p>DIV</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p>(<strong>ah</strong>， <strong>al</strong>) = (<strong>ax</strong> % <strong>r</strong>/m8， <strong>ax</strong> / <strong>r</strong>/m8)</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>DIV</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p>(<strong>dx</strong>, <strong>ax</strong>) = <strong>dx</strong>:<strong>ax</strong> / <strong>r</strong>/m16</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>DIV</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p>(<strong>edx</strong>, <strong>eax</strong>) = <strong>edx</strong>:<strong>eax</strong> / <strong>r</strong>/m32</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>IDIV</p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p>(<strong>ah</strong>， <strong>al</strong>) = <strong>ax</strong> / <strong>r</strong>/m8</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>IDIV</p></td>
<td align="left"><p><strong>r</strong>/m16</p></td>
<td align="left"><p>(<strong>dx</strong>, <strong>ax</strong>) = <strong>dx</strong>:<strong>ax</strong> / <strong>r</strong>/m16</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>IDIV</p></td>
<td align="left"><p><strong>r</strong>/m32</p></td>
<td align="left"><p>(<strong>edx</strong>, <strong>eax</strong>) = <strong>edx</strong>:<strong>eax</strong> / <strong>r</strong>/m32</p></td>
</tr>
</tbody>
</table>

 

未签名和签名除。 在伪代码说明中的第一个寄存器接收其余部分，而第二个接收商。 如果结果溢出目标，则生成除法溢出异常。

除法后的标志的状态为未定义。

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
<td align="left"><p>SET<em>cc</em></p></td>
<td align="left"><p><strong>r</strong>/m8</p></td>
<td align="left"><p>设置<strong>r</strong>/m8 为 0 或 1</p></td>
</tr>
</tbody>
</table>

 

如果条件*cc*为 true，则 8 位值设置为 1。 否则，8 位值设置为零。

### <a name="span-idbinary-codeddecimalspanspan-idbinary-codeddecimalspanspan-idbinary-codeddecimalspanbinary-coded-decimal"></a><span id="Binary-coded_Decimal"></span><span id="binary-coded_decimal"></span><span id="BINARY-CODED_DECIMAL"></span>二进制编码小数

除非正在调试以 COBOL 编写的代码，不会看到这些说明。

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
<td align="left"><p>添加后调整小数。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>DAS</p></td>
<td align="left"><p>小数调整后减法。</p></td>
</tr>
</tbody>
</table>

 

这些说明调整**al**执行已打包的二进制编码十进制操作后注册。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>AAA</p></td>
<td align="left"><p>ASCII 调整后添加。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AAS</p></td>
<td align="left"><p>ASCII 调整后减法。</p></td>
</tr>
</tbody>
</table>

 

这些说明调整**al**执行解压缩的二进制编码的十进制操作后注册。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>AAM</p></td>
<td align="left"><p>ASCII 调整后乘法。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AAD</p></td>
<td align="left"><p>相除后调整 ASCII。</p></td>
</tr>
</tbody>
</table>

 

这些说明调整**al**并**ah**执行解压缩的二进制编码的十进制操作后注册。

### <a name="span-idbitsspanspan-idbitsspanspan-idbitsspanbits"></a><span id="Bits"></span><span id="bits"></span><span id="BITS"></span>Bits

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
<td align="left"><p>和</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m 和<strong>r2</strong>/m/ #n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>或者</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m 或<strong>r2</strong>/m/ #n</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>异或</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p><strong>r1</strong>/m = <strong>r1</strong>/m xor <strong>r2</strong>/m/ #n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>NOT</p></td>
<td align="left"><p><strong>r1</strong>/m</p></td>
<td align="left"><p><strong>r1</strong>/m = 按位 not <strong>r1</strong>/m</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>测试</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>r2</strong>/m/ #n</p></td>
<td align="left"><p>计算<strong>r1</strong>/m 和<strong>r2</strong>/m/ #n</p></td>
</tr>
</tbody>
</table>

 

**测试**指令计算逻辑 AND 运算符和设置标志根据结果，但会抛弃结果。 通常跟测试的逻辑 and。 结果的条件跳转指令

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
<td align="left"><p><strong>r1</strong>/m， <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &lt;&lt;= <strong>cl</strong>/#n</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>SHR</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &gt;&gt;= <strong>cl</strong>/#n zero-fill</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>SAR</p></td>
<td align="left"><p><strong>r1</strong>/m， <strong>cl</strong>/#n</p></td>
<td align="left"><p><strong>r1</strong>/m &gt; &gt; =  <strong>cl</strong>/#n 符号填充</p></td>
</tr>
</tbody>
</table>

 

执行进位放置中移出的最后一个位。

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
<td align="left"><p><strong>r1</strong>， <strong>r2</strong>/m， <strong>cl</strong>/#n</p></td>
<td align="left"><p>Shift 左双引号。</p></td>
</tr>
</tbody>
</table>

 

Shift **r1**向左**cl**/\#n，使用的最高位填充**r2**/m。 执行进位放置中移出的最后一个位。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>SHRD</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r2</strong>/m， <strong>cl</strong>/#n</p></td>
<td align="left"><p>切换右两倍。</p></td>
</tr>
</tbody>
</table>

 

Shift **r1**向右**cl**/\#n，填充的底部位**r2**/m。 执行进位放置中移出的最后一个位。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ROL</p></td>
<td align="left"><p><strong>r1</strong>， <strong>cl</strong>/#n</p></td>
<td align="left"><p>旋转<strong>r1</strong>向左<strong>cl</strong>/#n。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ROR</p></td>
<td align="left"><p><strong>r1</strong>， <strong>cl</strong>/#n</p></td>
<td align="left"><p>旋转<strong>r1</strong>向右<strong>cl</strong>/#n。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RCL</p></td>
<td align="left"><p><strong>r1</strong>， <strong>cl</strong>/#n</p></td>
<td align="left"><p>旋转<strong>r1</strong>/C 左<strong>cl</strong>/#n。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RCR</p></td>
<td align="left"><p><strong>r1</strong>， <strong>cl</strong>/#n</p></td>
<td align="left"><p>旋转<strong>r1</strong>/C 右旋转<strong>cl</strong>/#n。</p></td>
</tr>
</tbody>
</table>

 

旋转是如移位，不同之处在于都被移出的位重新显示为传入填充位。 C 语言版本的旋转说明将携带位合并到旋转。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>BT</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r2</strong>/#n</p></td>
<td align="left"><p>复制位<strong>r2</strong>的 /#n <strong>r1</strong>携带到。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BTS</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r2</strong>/#n</p></td>
<td align="left"><p>设置位<strong>r2</strong>的 /#n <strong>r1</strong>，将以前的值复制到携带。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BTC</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r2</strong>/#n</p></td>
<td align="left"><p>清除位<strong>r2</strong>的 /#n <strong>r1</strong>，将以前的值复制到携带。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcontrolflowspanspan-idcontrolflowspanspan-idcontrolflowspancontrol-flow"></a><span id="Control_Flow"></span><span id="control_flow"></span><span id="CONTROL_FLOW"></span>控制流

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
<td align="left"><p>dest</p></td>
<td align="left"><p>分支条件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>JMP</p></td>
<td align="left"><p>dest</p></td>
<td align="left"><p>直接跳转。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>JMP</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>间接跳转。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>调用</p></td>
<td align="left"><p>dest</p></td>
<td align="left"><p>调用直接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>调用</p></td>
<td align="left"><p><strong>r</strong>/m</p></td>
<td align="left"><p>间接调用。</p></td>
</tr>
</tbody>
</table>

 

**调用**指令将推送到堆栈上的寄信人地址，然后跳转到目标。

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
<td align="left"><p><em>#n</em></p></td>
<td align="left"><p>返回</p></td>
</tr>
</tbody>
</table>

 

**Ret**指令弹出并跳转到回邮地址在堆栈上。 非零 *\#n*中**RET**指令指示弹出返回地址值后 *\#n*应添加到堆栈指针。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>循环</p></td>
<td align="left"><p>递减<strong>ecx</strong>和跳转如果结果为非零值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LOOPZ</p></td>
<td align="left"><p>递减<strong>ecx</strong> ，并跳转如果结果为非零值和<strong>zr</strong>设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LOOPNZ</p></td>
<td align="left"><p>递减<strong>ecx</strong> ，并跳转如果结果为非零值和<strong>zr</strong>已清除。</p></td>
</tr>
<tr class="even">
<td align="left"><p>JECXZ</p></td>
<td align="left"><p>如果跳转<strong>ecx</strong>为零。</p></td>
</tr>
</tbody>
</table>

 

这些说明是残留的 x86 的 CISC 遗产和最新的处理器中是写出这样的等效说明与实际速度较慢。

### <a name="span-idstringmanipulationspanspan-idstringmanipulationspanspan-idstringmanipulationspanstring-manipulation"></a><span id="String_Manipulation"></span><span id="string_manipulation"></span><span id="STRING_MANIPULATION"></span>字符串操作

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
<td align="left"><p>移动<em>T</em>从<strong>esi</strong>到<strong>edi。</strong></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>CMPS<em>T</em></p></td>
<td align="left"><p>比较<em>T</em>从<strong>esi</strong>与<strong>edi。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>SCAS<em>T</em></p></td>
<td align="left"><p>扫描<em>T</em>从<strong>edi</strong>为访问排序<em>t。</em></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>LOD<em>T</em></p></td>
<td align="left"><p>负载<em>T</em>从<strong>esi</strong>到 acc<em>t。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>STOS<em>T</em></p></td>
<td align="left"><p>应用商店<em>T</em>到<strong>edi</strong>从 acc<em>t。</em></p></td>
</tr>
</tbody>
</table>

 

在执行操作之后, 的源和目标寄存器是递增或递减的 sizeof (*T*)，根据方向标志 （增加或减少） 的设置。

指令可以加**REP**重复执行该操作指定的次数**ecx**注册。

**Rep mov**指令用于复制的内存块。

**Rep stos**指令用于填充访问排序的内存块*T*。

### <a name="span-idflagsspanspan-idflagsspanspan-idflagsspanflags"></a><span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>标志

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>LAHF</p></td>
<td align="left"><p>负载<strong>ah</strong>从标志。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SAHF</p></td>
<td align="left"><p>应用商店<strong>ah</strong>到标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STC</p></td>
<td align="left"><p>设置执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CLC</p></td>
<td align="left"><p>清除执行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CMC</p></td>
<td align="left"><p>补充携带。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STD</p></td>
<td align="left"><p>将方向设置为<em>下。</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLD</p></td>
<td align="left"><p>将方向设置为<em>向上。</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>STI</p></td>
<td align="left"><p>启用的中断。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLI</p></td>
<td align="left"><p>禁用中断。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinterlockedinstructionsspanspan-idinterlockedinstructionsspanspan-idinterlockedinstructionsspaninterlocked-instructions"></a><span id="Interlocked_Instructions"></span><span id="interlocked_instructions"></span><span id="INTERLOCKED_INSTRUCTIONS"></span>互锁的说明

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
<td align="left"><p>交换<strong>r1</strong>并<strong>r</strong>/m。</p></td>
</tr>
<tr class="even">
<td align="left"><p>XADD</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>添加<strong>r1</strong>到<strong>r</strong>/m，将原始值放在<strong>r1。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CMPXCHG</p></td>
<td align="left"><p><strong>r1</strong>， <strong>r</strong>/m</p></td>
<td align="left"><p>比较和交换条件。</p></td>
</tr>
</tbody>
</table>

 

**Cmpxchg**指令是原子的以下版本：

```asm
   cmp     accT, r/m
   jz      match
   mov     accT, r/m
   jmp     done
match:
   mov     r/m, r1
done:
```

### <a name="span-idmiscellaneousspanspan-idmiscellaneousspanspan-idmiscellaneousspanmiscellaneous"></a><span id="Miscellaneous"></span><span id="miscellaneous"></span><span id="MISCELLANEOUS"></span>杂项

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
<td align="left"><p><strong>r</strong>，m</p></td>
<td align="left"><p>如果捕获<strong>r</strong>不在范围内。</p></td>
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
<td align="left"><p>交换在寄存器中的字节顺序。</p></td>
</tr>
</tbody>
</table>

 

下面是一种特殊的情况**int**指令。

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
<td align="left"><p>调试器断点陷阱。</p></td>
</tr>
</tbody>
</table>

 

有关操作码**INT 3**是 0xCC。 有关操作码**NOP**是 0x90。

调试代码时，可能需要一些代码修补程序。 可以通过将有问题的字节替换 0x90 来执行此操作。

### <a name="span-ididiomsspanspan-ididiomsspanspan-ididiomsspanidioms"></a><span id="Idioms"></span><span id="idioms"></span><span id="IDIOMS"></span>Idioms

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
<td align="left"><p>异或</p></td>
<td align="left"><p><strong>r</strong>， <strong>r</strong></p></td>
<td align="left"><p><strong>r</strong> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em></strong></p></td>
<td align="left"><p>测试</p></td>
<td align="left"><p><strong>r</strong>， <strong>r</strong></p></td>
<td align="left"><p>如果选中<strong>r</strong> = 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>添加</p></td>
<td align="left"><p><strong>r</strong>， <strong>r</strong></p></td>
<td align="left"><p>Shift <strong>r</strong> 1 保留。</p></td>
</tr>
</tbody>
</table>

 

 

 






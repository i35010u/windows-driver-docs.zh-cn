---
title: 符号扩展
description: 符号扩展
keywords:
- 数字的符号扩展
- 寄存器的签名扩展
- MASM 表达式，签名扩展
- 寄存器、符号扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2a25f9589a963304e880b7eb4365521ee6b4673
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839933"
---
# <a name="sign-extension"></a>符号扩展


## <span id="ddk_sign_extension_dbg"></span><span id="DDK_SIGN_EXTENSION_DBG"></span>


如果32位有符号整数为负数，则其最大位等于1。 将此32位有符号整数强制转换为64位数字时，可以将高位设置为零 (保留数字的无符号整数和十六进制值) 或者可以将高位设置为保留数字) 的带符号值的一个 (。 后一种情况称为 " *符号扩展*"。

对于 MASM 表达式中的符号扩展、c + + 表达式和显示数字，调试器遵循不同的规则。

### <a name="span-idsign_extension_in_masm_expressionsspanspan-idsign_extension_in_masm_expressionsspansign-extension-in-masm-expressions"></a><span id="sign_extension_in_masm_expressions"></span><span id="SIGN_EXTENSION_IN_MASM_EXPRESSIONS"></span>MASM 表达式中的签名扩展

在某些情况下，由 MASM 表达式计算器自动对数字进行 *签名* 。 Sign extension 只能影响从0x80000000 到0xFFFFFFFF 的数字。 也就是说，符号扩展只会影响可以用32位编写，高位等于1的数字。

\`当调试器将其视为64位数字时，0x12345678 的数量始终保持为 0x00000000 12345678。 另一方面，当0x890ABCDE 被视为64位值时，它可能会保留 0x00000000 \` 890ABCDE，或者 MASM 表达式计算器可能会将其标记为 0xffffffff \` 890ABCDE。

从0x80000000 到0xFFFFFFFF 的数字根据以下条件进行了扩展：

-   在用户模式下，不会将数字常量标记为扩展。 在内核模式下，数字常量为 "已扩展"，除非它包含一个在 **\`** 低字节之前 ) 的抑音符 (。 例如，在内核模式下，十六进制数字 **EEAA1122** 和 **00000000EEAA1122** 为 sign extended，但 **00000000 \` EEAA1122** 和 **0 \` EEAA1122** 不是。

-   在这两种模式中，32位寄存器的签名已扩展。

-   伪寄存器始终存储为64位值。 它们不会在评估时进行扩展。 为伪寄存器 *分配* 值时，将根据标准 c + + 条件来计算使用的表达式。

-   表达式中的各个数字和寄存器都可以进行扩展，但在表达式计算期间，不会进行其他计算。 因此，你可以使用以下语法屏蔽数字或寄存器的高位。
    ```console
    ( 0x0`FFFFFFFF & expression )
    ```

### <a name="span-idsign_extension_in_c___expressionsspanspan-idsign_extension_in_c___expressionsspansign-extension-in-c-expressions"></a><span id="sign_extension_in_c___expressions"></span><span id="SIGN_EXTENSION_IN_C___EXPRESSIONS"></span>C + + 表达式中的签名扩展

调试器计算 c + + 表达式时，下列规则适用：

-   寄存器和伪寄存器决不会对扩展进行签名。

-   所有其他值都与 c + + 处理其类型的值完全相同。

### <a name="span-iddisplaying_sign_extended_and_64_bit_numbersspanspan-iddisplaying_sign_extended_and_64_bit_numbersspandisplaying-sign-extended-and-64-bit-numbers"></a><span id="displaying_sign_extended_and_64_bit_numbers"></span><span id="DISPLAYING_SIGN_EXTENDED_AND_64_BIT_NUMBERS"></span>显示 Sign-Extended 和64位数字

除32位和16位寄存器以外，所有数字都以64位值的形式存储在调试器内。 但是，当数字满足某些条件时，调试器会在命令输出中将其显示为32位数字。

调试器使用以下条件来确定如何显示数字：

-   如果数字的高32位全部为零 (也就是说，如果数字从 0x00000000 \` 00000000 到 0x00000000 \` FFFFFFFF) ，则调试器会将该数字显示为32位数字。

-   如果数字的高32位是全部，并且低32位的最高位也是一 (也就是说，如果该数字是从 0xFFFFFFFF \` 80000000 到 0xffffffff \` FFFFFFFF) ，则调试器假定该数字是一个带符号扩展的32位数字，并将其显示为一个32位数字。

-   如果前面的两个条件不应用 (也就是说，如果数字从 0x00000001 \` 00000000 到 0xffffffff 7FFFFFFF，则 \`) 调试器将该数字显示为64位数字。

由于这些显示规则，当数字显示为从0x80000000 到0xFFFFFFFF 的32位数字时，无法确认高32位是所有值还是全部为零。 若要区分这两种情况，您必须对数字执行附加计算 (例如屏蔽一个或多个高位并显示结果) 。

 

 






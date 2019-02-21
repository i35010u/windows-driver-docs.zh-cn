---
title: 符号扩展
description: 符号扩展
ms.assetid: 58e84d09-ab70-4cb2-b12f-4addb34f69d6
keywords:
- 符号扩展的数字
- 符号扩展的寄存器
- 符号扩展的 MASM 表达式
- 寄存器，符号扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bda170b255d20262e20db0cfc2be783f5ce4449
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525481"
---
# <a name="sign-extension"></a>符号扩展


## <span id="ddk_sign_extension_dbg"></span><span id="DDK_SIGN_EXTENSION_DBG"></span>


负 32 位有符号的整数时，其最高的位是等于 1。 当此 32 位有符号的整数转换为 64 位数字时，可以将高的位设置为零 （保留的无符号的整数和数字的十六进制值） 或可以将高的位设置为一个 （保留数的有符号的值）。 后一种情况称为*签名扩展*。

调试器遵循用于在 MASM 表达式中，在 c + + 表达式中，并显示数字的符号扩展不同规则。

### <a name="span-idsignextensioninmasmexpressionsspanspan-idsignextensioninmasmexpressionsspansign-extension-in-masm-expressions"></a><span id="sign_extension_in_masm_expressions"></span><span id="SIGN_EXTENSION_IN_MASM_EXPRESSIONS"></span>MASM 表达式中的符号扩展

某些情况下，数字是自动*符号扩展*MASM 表达式计算器。 符号扩展可能会影响仅通过 0xFFFFFFFF 0x80000000 中的数字。 也就是说，扩展会影响可以编写与高 32 位的数字的符号位等于 1。

数字 0x12345678 一直保持为 0x00000000\`12345678 时调试器将其视为一个 64 位数字。 但是，当 0x890ABCDE 视为一个 64 位值，它可能会保持 0x00000000\`890ABCDE 或 MASM 表达式计算器可能登录将其扩展到 0xFFFFFFFF\`890ABCDE。

通过 0xFFFFFFFF 0x80000000 中的数字的符号扩展基于以下条件：

-   数值常量永远不会是登录在用户模式下扩展。 在内核模式下，数值常量是扩展除非它包含的重读符号 ( **\`** ) 之前的低字节。 例如，在内核模式下，十六进制数字**EEAA1122**并**00000000EEAA1122**是符号扩展，但**00000000\`EEAA1122**和**0\`EEAA1122**不是。

-   32 位寄存器是在这两种模式中扩展的信号。

-   伪寄存器始终存储为 64 位值。 它们不是符号扩展时将计算它们。 伪寄存器，何时*分配*根据标准 c + + 标准计算一个值，使用的表达式。

-   单个数字和寄存器在表达式中的可以是登录扩展，但没有其他计算表达式计算期间登录扩展。 因此，可以屏蔽高位的数字或通过使用以下语法注册。
    ```console
    ( 0x0`FFFFFFFF & expression )
    ```

### <a name="span-idsignextensionincexpressionsspanspan-idsignextensionincexpressionsspansign-extension-in-c-expressions"></a><span id="sign_extension_in_c___expressions"></span><span id="SIGN_EXTENSION_IN_C___EXPRESSIONS"></span>在 c + + 表达式中的符号扩展

当调试器 c + + 表达式的计算结果时，以下规则适用：

-   寄存器和伪寄存器永远不会是扩展的登录。

-   C + + 想将其类型的值时一样，将被视为所有其他值。

### <a name="span-iddisplayingsignextendedand64bitnumbersspanspan-iddisplayingsignextendedand64bitnumbersspandisplaying-sign-extended-and-64-bit-numbers"></a><span id="displaying_sign_extended_and_64_bit_numbers"></span><span id="DISPLAYING_SIGN_EXTENDED_AND_64_BIT_NUMBERS"></span>显示符号扩展和 64 位数字

32 位和 16 位寄存器，以外所有数字都存储在内部该调试器内为 64 位值。 但是，当许多满足某些条件，调试器将其显示为命令输出中的 32 位数字。

调试器使用以下条件来确定如何显示数字：

-   许多高 32 位是否均为零 (即，如果数字是从 0x00000000\`00000000 通过 0x00000000\`FFFFFFFF)，调试器将数字显示为一个 32 位数字。

-   如果一个数字的高 32 位均为所有的选项和低 32 位的最高位也是一个 (即，如果数字是从 0xFFFFFFFF\`80000000 通过 0xFFFFFFFF\`FFFFFFFF)，调试器假定数是符号扩展 32 位数字，并将其显示为一个 32 位数字。

-   如果前面的两个条件不适用 (即，如果数字是从 0x00000001\`00000000 通过 0xFFFFFFFF\`7FFFFFFF) 调试器将数字显示为一个 64 位数字。

由于这些显示规则，当一个数字显示为通过 0xFFFFFFFF 0x80000000 中的 32 位数字，不能确认高 32 位是所有的选项或全为零。 若要区分这两种情况，必须在数字 （如一个或多个高的位掩码，并显示结果） 上执行其他计算。

 

 






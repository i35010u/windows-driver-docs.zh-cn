---
title: 源文件行语法
description: 源文件行语法
keywords:
- 表达式，源行号
- 源文件和路径，行号语法
- 行号语法
- 源文件和路径，文件名语法
- 文件名语法
- 命令的语法规则，源行号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cec161013490487f6185cb97258f39373c4eb2fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791621"
---
# <a name="source-line-syntax"></a>源文件行语法


## <span id="ddk_source_line_syntax_dbg"></span><span id="DDK_SOURCE_LINE_SYNTAX_DBG"></span>


可以指定源文件行号作为所有或部分 MASM 表达式。 这些数字的计算结果为对应于此源行的可执行代码的偏移量。

**注意**   不能使用源行号作为 c + + 表达式的一部分。 有关使用 MASM 和 c + + 表达式语法的详细信息，请参阅 [计算表达式](evaluating-expressions.md)。

 

您必须通过使用抑音符 ( ) 来将源文件和行号表达式括起来 **\`** 。 下面的示例显示了源文件行号的完整格式。

```text
`[[Module!]Filename][:LineNumber]`
```

如果有多个文件具有相同的文件名，则 *文件名* 应包括完整目录路径和文件名。 此目录路径应为编译时使用的路径。 如果只提供文件名或仅提供部分路径，并且有多个匹配项，则调试器将使用它找到的第一个匹配项。

如果省略 *Filename*，则调试器将使用与当前程序计数器相对应的源文件。

*LineNumber* 读取为十进制数字，除非在其前面加上 **0x**，而不考虑当前的默认基数。 如果省略 *LineNumber*，则表达式的计算结果为对应于源文件的可执行文件的初始地址。

不会在 CDB 中计算源行表达式，除非您发出了一个 [**(开关源行支持)**](-lines--toggle-source-line-support-.md) 命令，或者在启动 WinDbg 时包含 [**-line 命令行选项**](cdb-command-line-options.md) 。

有关源调试的详细信息，请参阅 [源模式下的调试](debugging-in-source-mode.md)。

 

 






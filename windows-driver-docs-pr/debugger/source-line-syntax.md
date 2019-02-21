---
title: 源行语法
description: 源行语法
ms.assetid: a4622a89-6419-4547-9650-eb10c3803462
keywords:
- 表达式中，源行号
- 源文件和行号语法的路径
- 行号语法
- 源代码文件和路径、 文件名语法
- 文件名语法
- 源行号的命令的语法规则
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f2595e618906116bbe89a05e91082d3051912a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527080"
---
# <a name="source-line-syntax"></a>源行语法


## <span id="ddk_source_line_syntax_dbg"></span><span id="DDK_SOURCE_LINE_SYNTAX_DBG"></span>


您可以指定为 MASM 表达式的全部或部分的源文件行号。 这些数字的计算结果为与此源行相对应的可执行代码的偏移量。

**请注意**  不能作为 c + + 表达式的一部分使用源行号。 有关使用 MASM 和 c + + 表达式语法的详细信息，请参阅[评估表达式](evaluating-expressions.md)。

 

必须通过抑音符将源代码文件和行号表达式 ( **\`** )。 下面的示例演示的完整格式为源文件行号。

```text
`[[Module!]Filename][:LineNumber]`
```

如果有多个文件具有相同的文件名称的*文件名*应包括整个目录路径和文件名。 此目录路径应为在编译时使用的那个。 如果您提供的文件的名称或部分路径，并且有多个匹配项，调试器将使用它找到的第一个匹配项。

如果省略*文件名*，调试器使用的源文件对应于当前的程序计数器。

*LineNumber*除非你在其与之前读取以十进制数**0x**，无论当前的默认基数。 如果省略*LineNumber*，表达式的计算结果与源文件相对应的可执行文件的初始地址。

除非您发出源行表达式不会评估中 CDB [ **.lines （切换源行支持）** ](-lines--toggle-source-line-support-.md)命令，或包括[ **-行命令行选项**](cdb-command-line-options.md)启动 WinDbg 时...

有关源调试的详细信息，请参阅[在源模式中进行调试](debugging-in-source-mode.md)。

 

 






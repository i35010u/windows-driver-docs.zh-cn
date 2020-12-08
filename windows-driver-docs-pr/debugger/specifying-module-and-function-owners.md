---
title: 指定模块和函数所有者
description: 指定模块和函数所有者
keywords:
- 可执行文件和路径，指定模块所有者
- 函数所有者
- 模块和函数的所有者
- triage.ini 文件
- triage.ini 文件，语法
- 分析扩展，triage.ini 文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d24896fc061111e63ce2c09992c435d174e71a03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785261"
---
# <a name="specifying-module-and-function-owners"></a>指定模块和函数所有者


## <span id="ddk_specifying_module_and_function_owners_dbg"></span><span id="DDK_SPECIFYING_MODULE_AND_FUNCTION_OWNERS_DBG"></span>


**！分析** 和 **！所有者** 扩展使用名为 Triage.ini 的文件来确定调试器遇到的符号的所有者。

使用这些扩展时，将在 "后续工作" 一词后显示函数或模块所有者的标识。

Triage.ini 文件是一个文本文件，该文件位于 \\ 用于 Windows 的调试工具安装的会审子目录中。 示例 Triage.ini 文件包含为 Windows 包调试工具的一部分。

**警告**   如果在与当前版本相同的目录中安装适用于 Windows 的调试工具的更新版本，则会覆盖该目录中的所有文件，包括 Triage.ini。 修改或替换 Triage.ini 文件的示例后，将其副本保存到其他目录。 重新安装调试器后，可以将保存的 Triage.ini 复制到默认版本。

 

### <a name="span-idformat_of_the_triage_ini_filespanspan-idformat_of_the_triage_ini_filespanformat-of-the-triageini-file"></a><span id="format_of_the_triage_ini_file"></span><span id="FORMAT_OF_THE_TRIAGE_INI_FILE"></span>Triage.ini 文件的格式

尽管 Triage.ini 文件旨在帮助你确定已分解到调试器中的函数的所有者，但此文件中的 "所有者" 字符串可能是任何有助于调试的内容。 字符串可以是编写或维护代码的人员的姓名。 或者，字符串可以是有关模块或函数中发生错误时可以执行的操作的简短说明。

此文件中的每行都具有以下语法。

```dbgcmd
Module[!Function]=Owner 
```

只能 \* 在模块或函数名的末尾添加星号 () 。 如果它出现在其他位置，则将其解释为文本字符。

不能在所有者字符串中添加空格。 如果所有者字符串中存在空格，则这些空格将被忽略。

有关语法选项的详细信息，请参阅特殊 Triage.ini 语法。

下面的示例演示 Triage.ini 文件示例。

```ini
module1=Person1
module2!functionA=Person2
module2!functionB=Person3
module2!funct*=Person4
module2!*=Person5
module3!singleFunction=Person6
mod*!functionC=Person7
```

### <a name="span-idtriage_ini_and__ownerspanspan-idtriage_ini_and__ownerspan-triageini-and-owner"></a><span id="triage_ini_and__owner"></span><span id="TRIAGE_INI_AND__OWNER"></span> Triage.ini 和！所有者

将模块或函数名传递给 [**！所有者**](-owner.md) 扩展时，调试器将显示 "后续" 一词，后跟模块或函数的所有者的名称。

下面的示例使用前面 Triage.ini 文件的示例。

```dbgcmd
0:000> !owner module2!functionB
Followup:  Person3
```

根据文件，"Person3" 拥有 **module2！ functionB**，"Person4" 拥有 **\\ module2！ funct** <em> 。 这两个字符串都与传递给 **！ owner** 的参数匹配，因此使用更完整的匹配。

### <a name="span-idtriage_ini_and__analyzespanspan-idtriage_ini_and__analyzespan-triageini-and-analyze"></a><span id="triage_ini_and__analyze"></span><span id="TRIAGE_INI_AND__ANALYZE"></span> Triage.ini 和！分析

使用 [**！分析**](-analyze.md) 扩展时，调试器会查看堆栈中排名最高的错误帧，并尝试确定此帧中的模块和函数的所有者。 如果调试器可以确定所有者，则会显示所有者信息。

如果调试器无法确定所有者，则调试器会传递到下一个堆栈帧，依此类推，直到调试器确定所有者或完全检查堆栈。

如果调试器可以确定所有者，所有者名称将显示在 "正在跟踪" 一词之后。 如果调试器在没有找到任何信息的情况下搜索整个堆栈，则不会显示任何名称。

下面的示例使用本主题前面给出的示例 Triage.ini 文件。

假设堆栈上的第一个帧是 **MyModule！ someFunction**。 调试器在 Triage.ini 文件中找不到 **MyModule** 。 接下来，它将继续到堆栈上的第二个帧中。

假设第二个帧是 **module3！ anotherFunction**。 调试器看不到 **module3** 的条目，但此模块中的 **anotherFunction** 不匹配。 接下来，调试器继续到第三个帧。

假设第三个帧是 **module2！ functionC**。 调试器首先查找完全匹配项，但这种匹配不存在。 然后，调试器会在 Triage.ini 中修整函数名称并发现 **module2！ funct \\** _。 此匹配将结束搜索，因为调试器确定所有者为 "Person4"。

调试器随后会显示类似于以下示例的输出。

```dbgcmd
0:000> !analyze
_******************************************************************************
*                                                                             *
*                        Exception Analysis                                   *
*                                                                             *
*******************************************************************************

Use !analyze -v to get detailed debugging information.

Probably caused by : module2 ( module2!functionC+15a )

Followup: Person4
---------
```

更完整的匹配优先于较短的匹配。 但是，与函数名称匹配始终首选模块名称匹配。 如果 **module2！ funct \\** _ 未在此 Triage.ini 文件中，则调试器会将 _*\\ module2！* *_ 选为匹配项。 如果已删除 _*module2！ funct \\* *_ 和 _*module2！ \\* *_ ，将选择 _ *mod \* ！ functionC**。

### <a name="span-idspecial_triage_ini_syntaxspanspan-idspecial_triage_ini_syntaxspanspecial-triageini-syntax"></a><span id="special_triage_ini_syntax"></span><span id="SPECIAL_TRIAGE_INI_SYNTAX"></span>特殊 Triage.ini 语法

如果省略惊叹号和函数名称，则添加 **！ \\** _ 在模块名称后，将显示该模块中的所有函数。 如果还单独指定了此模块中的函数，则优先使用更精确的规范。

如果将 "default" 用作模块名称或函数名称，则它等效于通配符。 例如， _*nt！ \\* *_ 与 _ * nt！默认值 * * 相同，**默认值** 与 **\* ！ \\ \*** 相同。

如果进行了匹配，但单词 **ignore** 出现在等号 (=) 右侧，则调试器会继续到堆栈中的下一帧。

可以在所有者名称之前添加 **最后一个 \_** 或 **可能 \_** 的。 当你运行 **！分析** 时，此前缀为所有者提供的优先级较低。 调试器在堆栈上 **的一个 \_ 较高的匹配** 项上选择较低的明确匹配项。 调试器还会选择 **\_** **\_** 堆栈上较低的匹配项，该匹配项在堆栈上的最后一个匹配项上方。

### <a name="span-idsample_triage_inispanspan-idsample_triage_inispansample-triageini"></a><span id="sample_triage_ini"></span><span id="SAMPLE_TRIAGE_INI"></span>示例 Triage.ini

"Windows 调试工具" 包中包含一个示例 Triage.ini 模板。 你可以将所需的任何模块和函数的所有者添加到此文件。 如果希望不使用全局默认值，请删除此文件开头的 **默认 = MachineOwner** 行。

 

 






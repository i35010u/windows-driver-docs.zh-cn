---
title: 指定模块和函数所有者
description: 指定模块和函数所有者
ms.assetid: be227712-7f70-4e74-b090-ca8b3ecd1e13
keywords:
- 可执行文件和路径，指定模块所有者
- 函数的所有者
- 模块和函数的所有者
- triage.ini 文件
- triage.ini 文件中语法
- 分析扩展，triage.ini 文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f27077d9553a11a96755abf3eb6897496bad6040
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368080"
---
# <a name="specifying-module-and-function-owners"></a>指定模块和函数所有者


## <span id="ddk_specifying_module_and_function_owners_dbg"></span><span id="DDK_SPECIFYING_MODULE_AND_FUNCTION_OWNERS_DBG"></span>


**！ 分析**并 **！ 所有者**扩展使用名为 Triage.ini 以确定调试器遇到的符号的所有者的文件。

当使用这些扩展时，"后续"一词之后显示函数或模块所有者的标识。

Triage.ini 文件是驻留在一个文本文件\\会审有关 Windows 调试工具安装子目录。 示例 Triage.ini 文件是作为有关 Windows 调试工具软件包的一部分。

**警告**  如果为当前版本的相同目录中安装的 Windows 调试工具的更新的版本，它将覆盖所有在该目录中包括 Triage.ini 文件。 修改或替换示例 Triage.ini 文件之后，它的副本保存到不同的目录。 重新安装调试程序后，可以将已保存的 Triage.ini 复制的默认版本。

 

### <a name="span-idformatofthetriageinifilespanspan-idformatofthetriageinifilespanformat-of-the-triageini-file"></a><span id="format_of_the_triage_ini_file"></span><span id="FORMAT_OF_THE_TRIAGE_INI_FILE"></span>Triage.ini 文件的格式

尽管 Triage.ini 文件旨在帮助您确定已分解成调试器函数的所有者，此文件中的"所有者"字符串可以是任何可能会帮助你进行调试。 字符串可以编写和维护代码的人员的名称。 或者，字符串类型可以是模块或函数中发生错误时可以执行有关的简短说明。

此文件中的每一行都具有以下语法。

```dbgcmd
Module[!Function]=Owner 
```

可以添加一个星号 (\*) 只能在模块或函数名称的末尾。 如果它出现在其他位置，则被解释为原义字符。

无法在所有者字符串中添加空间。 如果所有者字符串中确实存在空格，将忽略它们。

有关语法选项的详细信息，请参阅特殊 Triage.ini 语法。

以下示例显示了示例 Triage.ini 文件。

```ini
module1=Person1
module2!functionA=Person2
module2!functionB=Person3
module2!funct*=Person4
module2!*=Person5
module3!singleFunction=Person6
mod*!functionC=Person7
```

### <a name="span-idtriageiniandownerspanspan-idtriageiniandownerspan-triageini-and-owner"></a><span id="triage_ini_and__owner"></span><span id="TRIAGE_INI_AND__OWNER"></span> Triage.ini 和 ！ 所有者

当传递将模块或函数名称传递给[ **！ 所有者**](-owner.md)扩展，则调试器会显示的单词"后续"后跟该模块或函数的所有者的名称。

以下示例使用上面的示例 Triage.ini 文件。

```dbgcmd
0:000> !owner module2!functionB
Followup:  Person3
```

根据该文件，"Person3"拥有**module2 ！ functionB**，并"Person4"拥有**module2 ！ funct\\**<em>。这两个这些字符串匹配的参数传递给 **！ 所有者</em>*，因此使用更完整的匹配项。

### <a name="span-idtriageiniandanalyzespanspan-idtriageiniandanalyzespan-triageini-and-analyze"></a><span id="triage_ini_and__analyze"></span><span id="TRIAGE_INI_AND__ANALYZE"></span> Triage.ini 和 ！ 分析

当你使用[ **！ 分析**](-analyze.md)扩展，调试器会查看出错堆栈中的帧的顶部，并尝试确定模块和在此范围内的函数的所有者。 如果调试器可以确定所有者，则显示所有者信息。

如果调试器无法确定所有者，调试器将传递到下一步的堆栈帧，并完全检查等等，直到调试程序确定的所有者或堆栈。

如果调试器可以确定所有者，所有者名称将显示"后续"一词之后。 如果调试器没有找到的任何信息将搜索整个堆栈，没有显示任何名称。

以下示例使用本主题中前面提供的示例 Triage.ini 文件。

假设为堆栈上的第一帧**MyModule ！ someFunction**。 找不到调试器**MyModule** Triage.ini 文件中。 接下来，它将继续执行到堆栈上的第二个帧。

假设为第二个帧**module3 ！ anotherFunction**。 调试器 does 看到的条目**module3**，为没有匹配项，但**anotherFunction**此模块中。 接下来，调试器将继续执行到第三个帧。

假设为第三个帧**module2 ！ functionC**。 调试器首先查找完全匹配，但不是存在此类匹配。 调试器然后修剪函数名称，并发现**module2 ！ funct\\*** Triage.ini 中。 此匹配结束搜索，因为调试器确定所有者是"Person4"。

调试器就会显示类似于下面的示例的输出。

```dbgcmd
0:000> !analyze
*******************************************************************************
*                                                                             *
*                        Exception Analysis                                   *
*                                                                             *
*******************************************************************************

Use !analyze -v to get detailed debugging information.

Probably caused by : module2 ( module2!functionC+15a )

Followup: Person4
---------
```

更完整的匹配项优先于较短的匹配项。 但是，与匹配的模块名称是始终优先于函数名称匹配。 如果**module2 ！ funct\\*** 尚未在 Triage.ini 文件中，调试器将所选**module2 ！\\*** 作为匹配项。 如果这两个**module2 ！ funct\\*** 和**module2 ！\\*** 已删除**mod\*！ functionC**已选择。

### <a name="span-idspecialtriageinisyntaxspanspan-idspecialtriageinisyntaxspanspecial-triageini-syntax"></a><span id="special_triage_ini_syntax"></span><span id="SPECIAL_TRIAGE_INI_SYNTAX"></span>特殊 Triage.ini 语法

如果省略了感叹号和函数名称或添加 **！\\*** 后的模块名称，该模块中的所有函数来都指示。 如果还分别指定此模块内的某个函数，则更精确的规范优先。

如果"default"用作模块名称或函数名称，它相当于通配符字符。 例如， **nt ！\\*** 相同**nt ！ 默认**，和**默认**等同于 * *\*！\\***.

如果进行了匹配项，但该单词**忽略**显示右侧的等号 （=），调试器会继续到堆栈中的下一帧。

您可以添加**上次\_** 或**也许\_** 之前所有者的名称。 此前缀可以提供所有者更少的优先级运行时 **！ 分析**。 调试器选择是通过在堆栈上较低的明确匹配**也许\_** 是在堆栈上更高的匹配项。 调试器还会选择**也许\_** 是通过在堆栈上较低的匹配**上次\_** 是在堆栈上更高的匹配项。

### <a name="span-idsampletriageinispanspan-idsampletriageinispansample-triageini"></a><span id="sample_triage_ini"></span><span id="SAMPLE_TRIAGE_INI"></span>示例 Triage.ini

有关 Windows 调试工具包中包含示例 Triage.ini 模板。 可以将任何模块和所需的函数的所有者添加到此文件。 如果你想要有无全局默认值，删除**默认值 = MachineOwner**此文件开头的行。

 

 






---
title: 与引擎交互
description: 与引擎交互
ms.assetid: 80f5320f-ed34-4839-a16e-b3ff5d8edbfe
keywords:
- 调试器引擎 API，请使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c24df40a70030dfed450ba60a37f98a58f48928
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567088"
---
# <a name="interacting-with-the-engine"></a>与引擎交互


### <a name="span-idcommandsandexpressionsspanspan-idcommandsandexpressionsspancommands-and-expressions"></a><span id="commands_and_expressions"></span><span id="COMMANDS_AND_EXPRESSIONS"></span>命令和表达式

调试器引擎 API 提供了执行命令和计算表达式，如键入到 WinDbg 的方法[调试器命令窗口](the-debugger-command-window.md)。 若要执行的调试器命令，使用[ **Execute**](https://msdn.microsoft.com/library/windows/hardware/ff543208)。 或者，若要执行的所有命令在文件中，使用[ **ExecuteCommandFile**](https://msdn.microsoft.com/library/windows/hardware/ff543215)。

该方法[ **Evaluate** ](https://msdn.microsoft.com/library/windows/hardware/ff543046)将评估使用 c + + 或 MASM 语法的表达式。 调试器引擎中要计算表达式-例如所使用的语法**Evaluate**方法--由给定[ **GetExpressionSyntax** ](https://msdn.microsoft.com/library/windows/hardware/ff546701) ，可以使用更改[**SetExpressionSyntaxByName** ](https://msdn.microsoft.com/library/windows/hardware/ff556697)并[ **SetExpressionSyntax**](https://msdn.microsoft.com/library/windows/hardware/ff556696)。 将返回不同的语法识别的调试器数[ **GetNumberExpressionSyntaxes**](https://msdn.microsoft.com/library/windows/hardware/ff547913)，并返回其名称[ **GetExpressionSyntaxNames**](https://msdn.microsoft.com/library/windows/hardware/ff546708)。

返回的值的类型**Evaluate**由符号和已计算的字符串中使用的常量。 值包含在[**调试\_值**](https://msdn.microsoft.com/library/windows/hardware/ff541719)结构，并且可以强制转换为使用不同类型[ **CoerceValue** ](https://msdn.microsoft.com/library/windows/hardware/ff539158)并[ **CoerceValues**](https://msdn.microsoft.com/library/windows/hardware/ff539162)。

### <a name="span-idaliasesspanspan-idaliasesspanaliases"></a><span id="aliases"></span><span id="ALIASES"></span>别名

*别名*都是自动替换时调试器命令和表达式中使用其他字符字符串的字符字符串。 有关别名的概述，请参阅[Using 别名](using-aliases.md)。 调试器引擎具有别名的多个类。

*修复名称的别名*按数字编制索引，它们的名称**美元 u0**，**美元 u1**，...，**美元 u9**。 可以使用设置的值的这些别名[ **SetTextMacro** ](https://msdn.microsoft.com/library/windows/hardware/ff556809)方法，可以使用检索[ **GetTextMacro** ](https://msdn.microsoft.com/library/windows/hardware/ff549270)方法。

*自动别名*并*名用户为别名*可以具有任何名称。 由调试器引擎定义自动别名，用户通过调试器命令或调试器引擎 API 定义名为用户的别名。 若要定义或删除用户命名的别名，请使用[ **SetTextReplacement** ](https://msdn.microsoft.com/library/windows/hardware/ff556818)方法。 [ **GetTextReplacement** ](https://msdn.microsoft.com/library/windows/hardware/ff549280)方法返回的名称和值的自动别名或用户命名的别名。 可以使用删除所有用户命名的别名[ **RemoveTextReplacements** ](https://msdn.microsoft.com/library/windows/hardware/ff554548)方法。 [ **GetNumberTextReplacements** ](https://msdn.microsoft.com/library/windows/hardware/ff547988)方法将返回的用户名称和自动别名数; 这可以用于**GetTextReplacement**来循环访问所有这些别名。 [ **OutputTextReplacements** ](https://msdn.microsoft.com/library/windows/hardware/ff553268)方法将打印的所有用户命名别名，包括其名称和值的列表。

**请注意**  名用户为别名如果用户命名别名未指定相同的名称自动别名，将隐藏自动别名，以便按名称检索值的别名值，将使用名为用户的别名。

 

### <a name="span-idengineoptionsspanspan-idengineoptionsspanengine-options"></a><span id="engine_options"></span><span id="ENGINE_OPTIONS"></span>引擎选项

引擎具有多种选项可控制其行为。 中列出了这些选项[**调试\_ENGOPT\_XXX**](https://msdn.microsoft.com/library/windows/hardware/ff541475)。 返回的[ **GetEngineOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff546598) ，可使用设置[ **SetEngineOptions**](https://msdn.microsoft.com/library/windows/hardware/ff556670)。 可以使用设置的各个选项[ **AddEngineOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff537884)和取消设置使用[ **RemoveEngineOptions**](https://msdn.microsoft.com/library/windows/hardware/ff554491)。

### <a name="span-idinterruptsspanspan-idinterruptsspaninterrupts"></a><span id="interrupts"></span><span id="INTERRUPTS"></span>中断

中断是一种方法来强制中断到调试器或指示引擎停止处理当前命令，例如，通过在 WinDbg 中按 Ctrl + Break。

若要请求中断到调试器，或中断调试器的当前任务，请使用[ **SetInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff556722)。 若要检查是否已中断，请使用[ **GetInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff546944)。

**请注意**  调试器扩展从较长的任务时，建议扩展，接下来请**GetInterrupt**定期并停止处理如果请求了中断。

 

请求时中断到调试器，引擎可能会超时，如果需要对目标执行被侵入的情形而言太长。 如果目标是无响应状态，或者被侵入的情形请求被阻止或延迟资源争用，则可以发生此问题。 返回引擎要等待的时间长度[ **GetInterruptTimeout** ](https://msdn.microsoft.com/library/windows/hardware/ff546955) ，可使用设置[ **SetInterruptTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff556725)。

 

 






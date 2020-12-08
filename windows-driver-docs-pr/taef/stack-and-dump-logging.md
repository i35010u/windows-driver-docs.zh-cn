---
title: 堆栈和转储日志记录
description: 堆栈和转储日志记录
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77437173b2eea980661567723de4f92f3beab702
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796403"
---
# <a name="stack-and-dump-logging"></a>堆栈和转储日志记录


## <a name="span-idusing__stacktraceonerror_and__minidumponerror_switchesspanspan-idusing__stacktraceonerror_and__minidumponerror_switchesspanspan-idusing__stacktraceonerror_and__minidumponerror_switchesspanusing-stacktraceonerror-and-minidumponerror-switches"></a><span id="Using__stacktraceonerror_and__minidumponerror_switches"></span><span id="using__stacktraceonerror_and__minidumponerror_switches"></span><span id="USING__STACKTRACEONERROR_AND__MINIDUMPONERROR_SWITCHES"></span>使用/stacktraceonerror 和/minidumponerror 开关


可以通过两种方法从测试中捕获堆栈跟踪和小型转储。 最简单的方法是 "onerror" 模式。 运行测试时，请提供 te "/stacktraceonerror" 和/或 "/minidumponerror" 开关。 然后，如果遇到故障，记录器将使用默认格式捕获堆栈跟踪和/或小型转储。

捕获堆栈跟踪和小型转储的另一种方法是使用以下所述的 Api。

## <a name="span-idusing_wexdebugh_functionality_to_capture_stack_traces_and_mini_dumpsspanspan-idusing_wexdebugh_functionality_to_capture_stack_traces_and_mini_dumpsspanusing-wexdebugh-functionality-to-capture-stack-traces-and-mini-dumps"></a><span id="using_wexdebug.h_functionality_to_capture_stack_traces_and_mini_dumps"></span><span id="USING_WEXDEBUG.H_FUNCTIONALITY_TO_CAPTURE_STACK_TRACES_AND_MINI_DUMPS"></span>使用 WexDebug 功能捕获堆栈跟踪和小型转储


WexDebug 提供用于捕获调用堆栈跟踪和小型转储的 Api。

### <a name="span-idcall_savedump_api_to_save_a_mini_dumpspanspan-idcall_savedump_api_to_save_a_mini_dumpspanspan-idcall_savedump_api_to_save_a_mini_dumpspancall-savedump-api-to-save-a-mini-dump"></a><span id="Call_SaveDump_API_to_save_a_mini_dump."></span><span id="call_savedump_api_to_save_a_mini_dump."></span><span id="CALL_SAVEDUMP_API_TO_SAVE_A_MINI_DUMP."></span>调用 SaveDump API 以保存小型转储。

此 API 采用一个可选的 DWORD 参数 (这是一个转储类型标志或标记组合) 和一个字符串引用，在该参数中返回一个字符串，其中包含已保存转储文件的文件名和路径。 此文件名是由 API 自动生成的，并基于当前日期和时间。

可选转储类型参数指定拍摄的小型转储应包含的内容。 它还指定是将转储保存在 dmp 文件还是 cab 文件中，并且在 cab 文件中，是否将这些符号与转储一起保存。 如果省略可选参数，则使用默认设置。

示例 (将转储连同其 pdb) 一起保存到 cab 中：

```cpp
NoThrowString savedDumpFilePath;
HRESULT hr = Debug::SaveDump(MiniDumpFormat::WriteCab | MiniDumpFormat::WriteCabSecondaryFiles, savedDumpFilePath);
```

请注意，将转储保存到 cab 文件所用的时间比保存普通转储需要更长时间;附加符号文件甚至要花费更长的时间。

### <a name="span-idcall_getstack_api_to_obtain_a_call_stack_tracespanspan-idcall_getstack_api_to_obtain_a_call_stack_tracespanspan-idcall_getstack_api_to_obtain_a_call_stack_tracespancall-getstack-api-to-obtain-a-call-stack-trace"></a><span id="Call_GetStack_API_to_obtain_a_call_stack_trace."></span><span id="call_getstack_api_to_obtain_a_call_stack_trace."></span><span id="CALL_GETSTACK_API_TO_OBTAIN_A_CALL_STACK_TRACE."></span>调用 GetStack API 以获取调用堆栈跟踪。

此 API 采用一个可选的 DWORD 参数 (这是一个类型标志或标记组合) ，后者是一个字符串引用，其中包含当前上下文的调用堆栈跟踪。

可选的 stack 类型参数指定堆栈跟踪应该包含的内容。 如果省略可选参数，则使用默认设置。

示例：

```cpp
NoThrowString stackText;
HRESULT hr = Debug::GetStack(CallStackFormat::ColumnNames | CallStackFormat::FrameAddress |
                             CallStackFormat::SourceLine, stackText);
```

将堆栈选项标记与调试器命令相关联。 如果你使用 windbg 系列调试器，以下大致相关列表可能会很方便：


| 调试器语法 |          对应标志          |
|-----------------|---------------------------------------|
|        k        |     CallStackFormat：： ColumnNames      |
|       kv        |   k + CallStackFormat：： FunctionInfo   |
|     kp/kP     |    k + CallStackFormat：:P arameters    |
|       kn        |   k + CallStackFormat：： FrameNumbers   |
|       kf        | k + CallStackFormat：： FrameMemoryUsage |

## <a name="span-idtechnical_referencespanspan-idtechnical_referencespanspan-idtechnical_referencespantechnical-reference"></a><span id="Technical_Reference"></span><span id="technical_reference"></span><span id="TECHNICAL_REFERENCE"></span>技术参考


如果对有关转储和堆栈可选参数的详细信息感兴趣，请参阅随 [Windows 调试工具](https://go.microsoft.com/fwlink/p/?linkid=8708)提供的文档。 有关 "转储标志" 的文档，请参阅 [调试 \_ 格式 \_ XXX 文档](https://msdn.microsoft.com/library/cc267446.aspx)。 有关 "堆栈标志" 的文档，请参阅 ["OutputStackTrace" 方法文档](https://msdn.microsoft.com/library/cc266034.aspx)。










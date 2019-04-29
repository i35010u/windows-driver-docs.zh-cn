---
title: 堆栈和转储日志记录
description: 堆栈和转储日志记录
ms.assetid: 5FE6AA76-5299-4d5d-9154-6DB34D93EECB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58aeb88821a8ea4ba02dab7f41906a6fc84eeecb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386489"
---
# <a name="stack-and-dump-logging"></a>堆栈和转储日志记录


## <a name="span-idusingstacktraceonerrorandminidumponerrorswitchesspanspan-idusingstacktraceonerrorandminidumponerrorswitchesspanspan-idusingstacktraceonerrorandminidumponerrorswitchesspanusing-stacktraceonerror-and-minidumponerror-switches"></a><span id="Using__stacktraceonerror_and__minidumponerror_switches"></span><span id="using__stacktraceonerror_and__minidumponerror_switches"></span><span id="USING__STACKTRACEONERROR_AND__MINIDUMPONERROR_SWITCHES"></span>使用 /stacktraceonerror 和 /minidumponerror 切换


有两种方法可以捕获堆栈跟踪并从你的测试的微型转储。 最简单的方法是 onerror 模式。 在运行测试时提供 te / stacktraceonerror 和/或 / minidumponerror 开关。 然后，如果遇到故障时，记录器将捕获的堆栈跟踪和/或小型转储为您的默认格式。

要捕获堆栈跟踪和小型转储的其他方法是使用 Api，如下所述。

## <a name="span-idusingwexdebughfunctionalitytocapturestacktracesandminidumpsspanspan-idusingwexdebughfunctionalitytocapturestacktracesandminidumpsspanusing-wexdebugh-functionality-to-capture-stack-traces-and-mini-dumps"></a><span id="using_wexdebug.h_functionality_to_capture_stack_traces_and_mini_dumps"></span><span id="USING_WEXDEBUG.H_FUNCTIONALITY_TO_CAPTURE_STACK_TRACES_AND_MINI_DUMPS"></span>使用 WexDebug.h 功能捕获堆栈跟踪和小型转储


WexDebug.h 提供 Api 以捕获调用堆栈跟踪和微型转储。

### <a name="span-idcallsavedumpapitosaveaminidumpspanspan-idcallsavedumpapitosaveaminidumpspanspan-idcallsavedumpapitosaveaminidumpspancall-savedump-api-to-save-a-mini-dump"></a><span id="Call_SaveDump_API_to_save_a_mini_dump."></span><span id="call_savedump_api_to_save_a_mini_dump."></span><span id="CALL_SAVEDUMP_API_TO_SAVE_A_MINI_DUMP."></span>调用 SaveDump API，以保存微型转储。

此 API 采用一个可选参数，DWORD （即转储类型标志或标志组合） 和在其中它返回一个包含文件的名称和已保存的转储文件的路径字符串的字符串引用。 文件的名称自动生成 api 和基于当前日期和时间。

可选转储类型参数指定应包含哪些内容执行的小型转储。 它还指定是否转储将保存在 dmp 或 cab 文件，，指定的情况下 cab 文件，是否将转储一起保存符号。 如果省略了可选参数，则使用默认设置。

（保存到 cab 以及其 pdb 的转储） 的示例：

```cpp
NoThrowString savedDumpFilePath;
HRESULT hr = Debug::SaveDump(MiniDumpFormat::WriteCab | MiniDumpFormat::WriteCabSecondaryFiles, savedDumpFilePath);
```

请注意，，将转储保存到 cab 文件花费的时间超过保存普通转储;附加的符号文件将甚至更长时间。

### <a name="span-idcallgetstackapitoobtainacallstacktracespanspan-idcallgetstackapitoobtainacallstacktracespanspan-idcallgetstackapitoobtainacallstacktracespancall-getstack-api-to-obtain-a-call-stack-trace"></a><span id="Call_GetStack_API_to_obtain_a_call_stack_trace."></span><span id="call_getstack_api_to_obtain_a_call_stack_trace."></span><span id="CALL_GETSTACK_API_TO_OBTAIN_A_CALL_STACK_TRACE."></span>调用 GetStack API 来获取调用堆栈跟踪。

此 API 采用一个可选参数，DWORD (这是一种标志或标志组合) 和在其中它返回包含当前上下文的调用堆栈跟踪的字符串的字符串引用。

可选的堆栈类型参数指定应包含的堆栈跟踪。 如果省略了可选参数，则使用默认设置。

例如：

```cpp
NoThrowString stackText;
HRESULT hr = Debug::GetStack(CallStackFormat::ColumnNames | CallStackFormat::FrameAddress |
                             CallStackFormat::SourceLine, stackText);
```

调试器命令堆栈选项标记的关联。 如果使用 windbg 调试器系列以下大致的关联列表可能会派上用场：


| 调试器语法 |          相应的标志          |
|-----------------|---------------------------------------|
|        k        |     CallStackFormat::ColumnNames      |
|       kv        |   k + CallStackFormat::FunctionInfo   |
|     kp / kP     |    k + CallStackFormat::Parameters    |
|       kn        |   k + CallStackFormat::FrameNumbers   |
|       kf        | k + CallStackFormat::FrameMemoryUsage |

## <a name="span-idtechnicalreferencespanspan-idtechnicalreferencespanspan-idtechnicalreferencespantechnical-reference"></a><span id="Technical_Reference"></span><span id="technical_reference"></span><span id="TECHNICAL_REFERENCE"></span>技术参考


如果您感兴趣的转储和堆栈的可选参数的详细信息，请参阅附带的文档[有关 Windows 调试工具](https://go.microsoft.com/fwlink/p/?linkid=8708)。 有关转储标志详细信息，参阅的文档[调试\_格式\_XXX 文档](https://msdn.microsoft.com/library/cc267446.aspx)。 有关文档上的堆栈标志，请参阅[OutputStackTrace 方法文档](https://msdn.microsoft.com/library/cc266034.aspx)。










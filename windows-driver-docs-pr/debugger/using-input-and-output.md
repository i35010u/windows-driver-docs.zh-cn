---
title: 使用输入和输出
description: 使用输入和输出
ms.assetid: 7a23ee09-0314-400a-8152-eef49a225427
keywords:
- 调试器引擎、 输入和输出
- 输入和输出
- 输出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56040c8fc5bb4f7c4700f407391e095eec0f249b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366323"
---
# <a name="using-input-and-output"></a>使用输入和输出


## <span id="ddk_input_and_output_dbx"></span><span id="DDK_INPUT_AND_OUTPUT_DBX"></span>


调试器引擎中的输入和输出流的概述，请参阅[输入和输出](input-and-output.md)。

### <a name="span-idinputspanspan-idinputspaninput"></a><span id="input"></span><span id="INPUT"></span>输入

引擎将从所有客户端的输入要求如果[**输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol-input)在客户端上调用方法。 输入返回给调用方**输入**。

### <a name="span-idinput-callbacksspanspan-idinputcallbacksspaninput-callbacks"></a><span id="input-callbacks"></span><span id="INPUT_CALLBACKS"></span>输入的回调

当引擎请求从客户端的输入时，它使用[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebuginputcallbacks)向该客户端注册对象。 **IDebugInputCallbacks**可能与使用的客户端注册对象[ *SetInputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setinputcallbacks)。 每个客户端可以具有最多**IDebugInputCallbacks**对象注册到它。

输入请求开头引擎调用[ **IDebugInputCallbacks::StartInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebuginputcallbacks-startinput)方法。 这会通知**IDebugInputCallbacks**引擎现在正在等待输入的对象。

如果**IDebugInputCallbacks**对象中的一些输入引擎，它可以调用[ **ReturnInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-returninput)的任何客户端的方法。 一次**ReturnInput**调用方法，该引擎将不会再输入。 此方法的后续调用方将不接收输入通知。

该引擎将调用[ **IDebugInputCallbacks::EndInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebuginputcallbacks-endinput)以指示它已停止等待输入。

最后，引擎将回显到已注册此输入**IDebugOutputCallbacks**对象 （除了用来提供输入的一个） 的每个客户端通过使用[ **idebugoutputcallbacks:: Output**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugoutputcallbacks-output)带有位掩码设置为调试\_输出\_提示。

### <a name="span-idoutputspanspan-idoutputspanoutput"></a><span id="output"></span><span id="OUTPUT"></span>输出

可能会将输出发送到该引擎使用多个客户端方法--例如[*输出*](https://msdn.microsoft.com/library/windows/hardware/ff553183)并[ *OutputVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputvalist)。 一旦收到输出，则引擎将其发送到某些客户端。

客户端使用*输出掩码*以指示哪些类型的输出他们感兴趣。 只要引擎生成输出，它均附带一个掩码，指定其输出类型。 如果输出的类型匹配的客户端的输出掩码，客户端将接收输出。 可以通过调用设置的输出掩码[ **SetOutputMask** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setoutputmask)和使用查询[ **GetOutputMask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getoutputmask)。 请参阅[**调试\_输出\_XXX** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-output-xxx)的输出掩码值的详细信息。

由控制客户端列表，引擎将发送到输出*输出控制*。 通常情况下，设置输出控制要将输出发送给所有客户端;但是，它可以暂时使用更改[ *ControlledOutput* ](https://msdn.microsoft.com/library/windows/hardware/ff539248)并[ *ControlledOutputVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-controlledoutputvalist)。 请参阅[**调试\_OUTCTL\_XXX** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-outctl-xxx)输出控制值有关的详细信息。

输出可能缓冲的引擎。 如果多个小的输出传递到引擎中，它可能会收集它们并将其发送到客户端中的一个大段内。 若要刷新此缓冲区，请使用[ **FlushCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-flushcallbacks)。

每个客户端对象具有*输出宽度*，这是客户端对象的输出显示的宽度。 尽管此宽度仅使用作为提示，但某些命令和扩展函数设置格式基于此宽度其输出。 宽度 GetOutputWidth 方法返回，可以使用 SetOutputWidth 方法进行设置。

### <a name="span-idoutput-callbacksspanspan-idoutputcallbacksspanoutput-callbacks"></a><span id="output-callbacks"></span><span id="OUTPUT_CALLBACKS"></span>输出回调

当引擎将输出发送到客户端时，它使用[IDebugOutputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugoutputcallbacks)对象注册客户端。 **IDebugOutputCallbacks**可能与使用的客户端注册对象[ *SetOutputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setoutputcallbacks)。 每个客户端可以具有最多**IDebugInputCallbacks**对象注册到它。

若要发送的输出，则引擎将调用[ **idebugoutputcallbacks:: Output** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugoutputcallbacks-output)方法。

### <a name="span-idoutput-line-prefixspanspan-idoutputlineprefixspanoutput-line-prefix"></a><span id="output-line-prefix"></span><span id="OUTPUT_LINE_PREFIX"></span>输出行的前缀

每个客户端对象具有*输出行的前缀*其附加到每个行的输出发送到客户端对象与关联的输出回调。 这可以用于缩进或输出的每一行上放置标识标记。

输出行的前缀返回的 GetOutputLinePrefix，可以使用 SetOutputLinePrefix 进行设置。 若要暂时更改输出行的前缀和更高版本更改回去，请使用 PushOutputLinePrefix 和 PopOutputLinePrefix。

### <a name="span-idlog-filesspanspan-idlogfilesspanlog-files"></a><span id="log-files"></span><span id="LOG_FILES"></span>日志文件

调试器引擎支持打开一个日志文件来记录调试会话。 最多一个日志文件可以一次打开。 输出发送到输出回调也发送到此日志文件 （除非它标记为不会记录）。

若要打开日志文件，请使用[ **OpenLogFile2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-openlogfile2) (或[ **OpenLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-openlogfile))。 该方法[ **GetLogFile2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getlogfile2) (或[ **GetLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getlogfile)) 返回当前打开的日志文件。 若要关闭日志文件，请使用[ **CloseLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-closelogfile)。

该方法[ **SetLogMask** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setlogmask)可用于筛选将输出发送到日志文件，并[ **GetLogMask** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getlogmask)将返回当前的日志文件筛选器。

### <a name="span-idpromptspanspan-idpromptspanprompt"></a><span id="prompt"></span><span id="PROMPT"></span>提示

交互式调试会话中提示可用于向用户指示调试器正在等待用户输入。 在提示符下发送到使用的输出回调[ *OutputPrompt* ](https://msdn.microsoft.com/library/windows/hardware/ff553227)并[ *OutputPromptVaList* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputpromptvalist)方法。 返回标准的提示的内容[ **GetPromptText**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getprompttext)。

 

 






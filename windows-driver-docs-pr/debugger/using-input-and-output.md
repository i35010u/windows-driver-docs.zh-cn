---
title: 使用输入和输出
description: 使用输入和输出
ms.assetid: 7a23ee09-0314-400a-8152-eef49a225427
keywords:
- 调试器引擎、输入和输出
- 输入和输出
- 输出
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37e695f7f9c6bd47f27857bb4f62cd22f98926c5
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534754"
---
# <a name="using-input-and-output"></a>使用输入和输出


## <span id="ddk_input_and_output_dbx"></span><span id="DDK_INPUT_AND_OUTPUT_DBX"></span>


有关调试器引擎中输入和输出流的概述，请参阅[输入和输出](input-and-output.md)。

### <a name="span-idinputspanspan-idinputspaninput"></a><span id="input"></span><span id="INPUT"></span>送

如果在客户端调用了[**输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol-input)法，则引擎将要求其所有客户端提供输入。 输入将返回到**输入**的调用方。

### <a name="span-idinput-callbacksspanspan-idinput_callbacksspaninput-callbacks"></a><span id="input-callbacks"></span><span id="INPUT_CALLBACKS"></span>输入回调

当引擎要求客户端提供输入时，它将使用已注册到该客户端的[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebuginputcallbacks)对象。 可以使用[*SetInputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setinputcallbacks)将**IDebugInputCallbacks**对象注册到客户端。 每个客户端最多只能向其中注册一个**IDebugInputCallbacks**对象。

输入请求从引擎开始，调用[**IDebugInputCallbacks：： StartInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebuginputcallbacks-startinput)方法。 这会通知**IDebugInputCallbacks**对象引擎现在正在等待输入。

如果**IDebugInputCallbacks**对象包含引擎的某些输入，则它可以调用任何客户端的[**ReturnInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-returninput)方法。 调用**ReturnInput**方法后，引擎将不会再进行任何输入。 此方法的后续调用方将收到未收到输入的通知。

然后，引擎将调用[**IDebugInputCallbacks：： EndInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebuginputcallbacks-endinput)以指示它已停止等待输入。

最后，引擎将此输入回显到每个客户端（用于提供输入的每个客户端除外）的已注册**IDebugOutputCallbacks**对象，方法是使用[**IDebugOutputCallbacks：： Output**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugoutputcallbacks-output) ，并将位掩码设置为调试 \_ 输出 \_ 提示符。

### <a name="span-idoutputspanspan-idoutputspanoutput"></a><span id="output"></span><span id="OUTPUT"></span>输出

可以使用多个客户端方法将输出发送到引擎，例如[*output*](https://msdn.microsoft.com/library/windows/hardware/ff553183)和[*OutputVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputvalist)。 接收到输出后，引擎会将其发送到一些客户端。

客户端使用*输出掩码*来指示它们感兴趣的输出类型。 只要引擎生成输出，就会附带指定其输出类型的掩码。 如果输出的类型与客户端的输出掩码匹配，则客户端将接收输出。 可以通过调用[**SetOutputMask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setoutputmask)来设置输出掩码，并使用[**GetOutputMask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getoutputmask)进行查询。 有关输出掩码值的详细信息，请参阅[**调试 \_ 输出 \_ XXX**](debug-output-xxx.md) 。

引擎将向其发送输出的客户端列表由*输出控件*控制。 通常，输出控件设置为将输出发送到所有客户端;但是，可以使用[*ControlledOutput*](https://msdn.microsoft.com/library/windows/hardware/ff539248)和[*ControlledOutputVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-controlledoutputvalist)临时更改此方法。 有关输出控制值的详细信息，请参阅[**DEBUG \_ OUTCTL \_ XXX**](debug-outctl-xxx.md) 。

引擎可以缓冲输出。 如果将多个输出传递到引擎，则可以收集这些输出，并将其发送到一个大块的客户端。 若要刷新此缓冲区，请使用[**FlushCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-flushcallbacks)。

每个客户端对象都有*输出宽度*，即客户端对象的输出显示的宽度。 虽然此宽度仅用作提示，但某些命令和扩展函数会根据此宽度设置其输出的格式。 宽度由 GetOutputWidth 方法返回，可使用 SetOutputWidth 方法进行设置。

### <a name="span-idoutput-callbacksspanspan-idoutput_callbacksspanoutput-callbacks"></a><span id="output-callbacks"></span><span id="OUTPUT_CALLBACKS"></span>输出回调

当引擎将输出发送到客户端时，它将使用已注册到客户端的[IDebugOutputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugoutputcallbacks)对象。 可以使用[*SetOutputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setoutputcallbacks)将**IDebugOutputCallbacks**对象注册到客户端。 每个客户端最多只能向其中注册一个**IDebugInputCallbacks**对象。

为了发送输出，引擎将调用[**IDebugOutputCallbacks：： output**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugoutputcallbacks-output)方法。

### <a name="span-idoutput-line-prefixspanspan-idoutput_line_prefixspanoutput-line-prefix"></a><span id="output-line-prefix"></span><span id="OUTPUT_LINE_PREFIX"></span>输出行前缀

每个客户端对象都有一个*输出行前缀*，该前缀将追加到发送到与客户端对象相关联的输出回调的每个输出行。 这可用于缩进，或在每个输出行上放置标识标记。

输出行前缀由 GetOutputLinePrefix 返回，可使用 SetOutputLinePrefix 进行设置。 若要暂时更改输出行前缀，稍后再将其更改回，请使用 PushOutputLinePrefix 和 PopOutputLinePrefix。

### <a name="span-idlog-filesspanspan-idlog_filesspanlog-files"></a><span id="log-files"></span><span id="LOG_FILES"></span>日志文件

调试器引擎支持打开日志文件来记录调试会话。 一次最多可以打开一个日志文件。 发送到输出回调的输出也将发送到此日志文件（除非已将其标记为不记录）。

若要打开日志文件，请使用[**OpenLogFile2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-openlogfile2) （或[**OpenLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-openlogfile)）。 方法[**GetLogFile2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getlogfile2) （或[**GetLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getlogfile)）返回当前打开的日志文件。 若要关闭日志文件，请使用[**CloseLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-closelogfile)。

方法[**SetLogMask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setlogmask)可用于筛选发送到日志文件的输出， [**GetLogMask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getlogmask)将返回当前日志文件筛选器。

### <a name="span-idpromptspanspan-idpromptspanprompt"></a><span id="prompt"></span><span id="PROMPT"></span>处

在交互式调试会话中，可使用提示符向用户指示调试器正在等待用户输入。 使用[*OutputPrompt*](https://msdn.microsoft.com/library/windows/hardware/ff553227)和[*OutputPromptVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputpromptvalist)方法将提示发送到输出回调。 标准提示符的内容由[**GetPromptText**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getprompttext)返回。

 

 






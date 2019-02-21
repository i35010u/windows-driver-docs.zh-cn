---
title: 在调试器中的示例 16 查看跟踪消息
description: 在调试器中的示例 16 查看跟踪消息
ms.assetid: c548643c-ae0c-47e7-af0a-0d89ed78f281
keywords:
- 跟踪消息显示 WDK
- 显示跟踪消息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 393da6d1968da18c793ce9000a441c546d03e067
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519578"
---
# <a name="example-16-viewing-trace-messages-in-a-debugger"></a>示例 16:在调试器中查看跟踪消息


## <span id="ddk_viewing_trace_messages_in_a_debugger_tools"></span><span id="DDK_VIEWING_TRACE_MESSAGES_IN_A_DEBUGGER_TOOLS"></span>


此示例演示如何重定向跟踪消息，KD 或 WinDbg。

在开始之前跟踪会话，验证 Wmitrace.dll 和 Traceprt.dll 是在主计算机上的调试程序的搜索路径中。 中包含这些 Dll[有关 Windows 调试工具](https://go.microsoft.com/fwlink/p/?linkid=8708)中\\Program Files\\有关 Windows 调试工具\\winxp 目录。 （虽然在但目录名称，文件使用在 Windows 2000 和更高版本的 Windows。）

此外，检查是否[跟踪消息格式文件](trace-message-format-file.md)(TMF) 跟踪提供程序是在调试器的搜索路径中。

若要设置的调试程序的搜索路径，请使用 ！ wmitrace.searchpath 专用调试器扩展，或设置的值 %跟踪\_格式\_搜索\_PATH %环境变量。 例如：

```
set TRACE_FORMAT_SEARCH_PATH=c:\tracing
```

然后，启动调试器。 如果提交的跟踪日志命令 **-kd**参数，并且调试程序未运行，Tracelog 停止响应 （"挂起"）。

以下命令启动跟踪会话，并将跟踪消息发送到 KD 或的 Windbg 中，附加者为准。

```
tracelog -start MyTrace -guid MyProvider.ctl -rt -kd
```

**Tracelog-启动**命令包含要启动跟踪会话的会话名称。 它使用**guid**参数来标识提供程序文件。 它还使用 **-rt**参数来启动实时跟踪会话，以便跟踪消息发送到调试器并不是指向日志文件。

在响应中，跟踪日志报告它已启动会话。 跟踪提供程序生成的消息，消息会显示在调试器中。

若要在调试器中查看消息，请使用 WMI 跟踪扩展。 有关信息，请参阅[有关 Windows 调试工具](https://go.microsoft.com/fwlink/p/?linkid=8708)。

 

 






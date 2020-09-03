---
title: 示例16在调试器中查看跟踪消息
description: 示例16在调试器中查看跟踪消息
ms.assetid: c548643c-ae0c-47e7-af0a-0d89ed78f281
keywords:
- 显示 WDK 的跟踪消息
- 显示跟踪消息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95eb49b026ed98bd88e4be979507f562d5dd54b5
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383455"
---
# <a name="example-16-viewing-trace-messages-in-a-debugger"></a>示例 16：在调试器中查看跟踪消息


## <span id="ddk_viewing_trace_messages_in_a_debugger_tools"></span><span id="DDK_VIEWING_TRACE_MESSAGES_IN_A_DEBUGGER_TOOLS"></span>


此示例演示如何将跟踪消息重定向到 KD 或 WinDbg。

在开始跟踪会话之前，验证 Wmitrace.dll 和 Traceprt.dll 是否在主计算机上的调试器搜索路径中。 这些 Dll 包含在 windows [调试](../debugger/debugger-download-tools.md) 工具的 "用于 \\ windows Winxp 的程序文件 \\ 调试工具" \\ 目录中。 尽管目录名称 (，但文件在 Windows 2000 和更高版本的 Windows 中工作。 ) 

同时，验证跟踪提供程序 (TMF) 的 [跟踪消息格式文件](trace-message-format-file.md) 是否在调试器的搜索路径中。

若要设置调试器的搜索路径，请使用！ searchpath 专用调试程序扩展或设置% 跟踪 \_ 格式 \_ 搜索 \_ 路径% 环境变量的值。 例如：

```
set TRACE_FORMAT_SEARCH_PATH=c:\tracing
```

然后，启动调试器。 如果提交带有 **-kd** 参数的 Tracelog 命令，但调试器未运行，则 Tracelog 将停止响应 ( "挂起" ) 。

下面的命令启动一个跟踪会话，并将跟踪消息发送到 KD 或 Windbg （以附加的形式）。

```
tracelog -start MyTrace -guid MyProvider.ctl -rt -kd
```

**Tracelog**命令包含用于启动跟踪会话的会话名称。 它使用 **-guid** 参数标识提供程序文件。 它还使用 **-rt** 参数启动实时跟踪会话，以便将跟踪消息发送到调试器，而不是发送到日志文件。

在响应中，Tracelog 报告它已启动了会话。 当跟踪提供程序生成消息时，消息将出现在调试器中。

若要在调试器中查看这些消息，请使用 WMI 跟踪扩展。 有关信息，请参阅 [Windows 调试工具](../debugger/index.md)。

 


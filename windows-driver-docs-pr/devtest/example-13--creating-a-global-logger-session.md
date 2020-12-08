---
title: 示例13创建全局记录器会话
description: 示例13创建全局记录器会话
keywords:
- 跟踪会话 WDK，全局记录器
- 全局记录器跟踪会话 WDK，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97ab07bc8d049a84d732267af93747f7a78a58bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839149"
---
# <a name="example-13-creating-a-global-logger-session"></a>示例 13：创建全局记录器会话


## <span id="ddk_controlling_a_global_logger_session_tools"></span><span id="DDK_CONTROLLING_A_GLOBAL_LOGGER_SESSION_TOOLS"></span>


[全局记录器跟踪会话](global-logger-trace-session.md)与其他跟踪会话不同，后者从注册表项中读取其配置参数。 由于 Tracelog 会为你处理这些差异，因此用于启动和停止全局记录器跟踪会话的命令与其他会话不同。 但是，你不能更新全局记录器会话，并且在停止会话后，必须使用 **tracelog** 命令重置为会话创建的注册表项。

此外， **tracelog** 命令不启动跟踪会话;它仅创建并配置它。 当你重新启动系统时，会话启动。

以下命令是用于配置全局记录器会话的最简单的命令。 它将 **tracelog** 命令与保留的 **GlobalLogger** 名称一起使用。 Tracelog 对所有其他参数使用默认值。

```
tracelog -start GlobalLogger
```

作为响应，Tracelog 将在 **HKLM \\ SYSTEM \\ CurrentControlSet \\ Control \\ WMI** 中创建 **GlobalLogger** 子项，其中包含每个参数的注册表项。 它在子项中创建 **开始** 项并将其值设置为 \` 1。

由于该命令不包含 **-f** 参数，此会话的跟踪日志存储在全局记录器跟踪会话的默认位置，% SystemRoot% \\ System32 日志 \\ \\ \\ 记录 WMI trace .log。 若要查看日志，请将 [Tracefmt](tracefmt.md) 或 [TraceView](traceview.md) 与 tmf[跟踪消息格式文件](trace-message-format-file.md)一起使用。

配置会话后，重新启动系统以启动跟踪会话。

以下命令将停止跟踪会话，但不会影响注册表项。

```
tracelog -stop GlobalLogger
```

然后，若要重置注册表项，请使用以下命令。

```
tracelog -remove GlobalLogger
```

此命令删除可选参数的任何注册表项（在此) 示例中为 "无"） (。 它保留 **GlobalLogger** 子项和 **start** 条目，但它会将 **start** 的值设置为 0 (不启动) 。

**Tracelog-remove** 命令不是必需的。 你可以在注册表中保留这些项，并在下次运行全局记录器跟踪会话时使用它们。 如果用不同的参数启动会话，Tracelog 会将注册表项的值替换为 **Tracelog-start** 命令中指定的值。

 

 






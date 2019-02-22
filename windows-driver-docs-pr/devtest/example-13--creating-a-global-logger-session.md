---
title: 示例 13 创建全局记录器会话
description: 示例 13 创建全局记录器会话
ms.assetid: 11574df3-817e-4bf3-a849-dd5ac723fb1d
keywords:
- 跟踪会话 WDK，全局记录器
- 全局记录器跟踪会话 WDK，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a42d62abc4e6f4866354fd253d3551805daecec2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547119"
---
# <a name="example-13-creating-a-global-logger-session"></a>示例 13:创建全局记录器会话


## <span id="ddk_controlling_a_global_logger_session_tools"></span><span id="DDK_CONTROLLING_A_GLOBAL_LOGGER_SESSION_TOOLS"></span>


一个[全局记录器跟踪会话](global-logger-trace-session.md)不同于其他跟踪会话，因为它从注册表项读取其配置参数。 Tracelog 为你处理这些差异，因为用于启动和停止全局记录器跟踪会话的命令与无显著差异与用于其他会话。 但是，无法更新全局记录器会话，并且之后停止会话，必须使用**tracelog-删除**命令重置为会话创建的注册表项。

此外， **tracelog-启动**命令不会启动跟踪会话; 它只需创建并配置它。 在会话启动时重新启动系统。

以下命令是最简单配置全局记录器会话的命令。 它使用**tracelog-开始**命令以保留**GlobalLogger**名称。 跟踪日志的所有其他参数使用的默认值。

```
tracelog -start GlobalLogger
```

在响应中，创建 Tracelog **GlobalLogger**子项中**HKLM\\系统\\CurrentControlSet\\控制\\WMI**与注册表项为每个参数。 它会创建**启动**子项中的条目并将其值设置为\`1。

由于该命令未包括 **-f**参数，此会话的跟踪日志的默认位置中存储的全局记录器跟踪会话，%systemroot%\\System32\\LogFiles\\WMI\\trace.log。 若要查看日志，请使用[Tracefmt](tracefmt.md)或[TraceView](traceview.md)与 System.tmf[跟踪消息格式文件](trace-message-format-file.md)。

将会话配置后，重新启动系统重新启动跟踪会话。

以下命令停止跟踪会话，但它不影响注册表项。

```
tracelog -stop GlobalLogger
```

然后，若要重置的注册表项，请使用以下命令。

```
tracelog -remove GlobalLogger
```

此命令删除可选参数 （无，在此情况下） 任何注册表项。 离开**GlobalLogger**子项并**启动**注册表项，但它的值设置**启动**为 0 （不启动）。

**Tracelog-删除**命令不是必需。 可以在注册表中的条目不并使用它们在下次运行全局记录器跟踪会话。 如果使用不同的参数启动会话时，Tracelog 替换的值的注册表项中指定的值**tracelog-启动**命令。

 

 






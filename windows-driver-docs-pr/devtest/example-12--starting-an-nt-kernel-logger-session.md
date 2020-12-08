---
title: 示例12启动 NT 内核记录器会话
description: 示例12启动 NT 内核记录器会话
keywords:
- 跟踪会话 WDK，NT 内核记录器
- NT 内核记录器跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d403d7eb05db8f1a89de8ad76c01c978645cfdf6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839153"
---
# <a name="example-12-starting-an-nt-kernel-logger-session"></a>示例 12：启动 NT 内核记录器会话


## <span id="ddk_starting_an_nt_kernel_logger_session_tools"></span><span id="DDK_STARTING_AN_NT_KERNEL_LOGGER_SESSION_TOOLS"></span>


下面的命令启动 NT 内核记录器跟踪会话。 由于 NT 内核记录器跟踪会话是默认值，因此不需要其他参数。

```
tracelog -start
```

默认情况下，将跟踪进程、线程、磁盘和 TCP/IP 事件。 若要覆盖默认值，可以使用为 NT 内核记录器会话设计的参数。

以下命令使用 **-nothread** 参数来关闭线程事件的跟踪，使用 **-hf** 参数来跟踪硬页面错误，并使用 **-cm** 参数跟踪注册表事件。 此示例还使用可选的 **-ft** 参数，该参数可在任何跟踪会话中使用，以在固定时间间隔刷新缓冲区，以及当缓冲区已满时进行自动刷新。

```
tracelog -start -nothread -hf -cm -ft 2
```

还可以使用 NT 内核记录器启动实时跟踪会话。 以下命令使用 NT 内核记录器启动实时跟踪会话。 同样，如前面的示例中所示，可以省略会话名称，因为 "NT 内核记录器" 是默认值。

```
tracelog -start -rt
```

除了自定义缓冲区的参数和计时器分辨率外，还可以对实时跟踪会话使用自定义的 NT 内核记录器参数。

若要格式化并显示此会话中的跟踪消息，请使用 Tracefmt。 以下命令在命令提示符窗口中显示来自 NT 内核记录器会话的跟踪消息。 有关详细信息，请参阅 [Tracefmt](tracefmt.md)。

```
tracefmt -rt -display
```

 

 






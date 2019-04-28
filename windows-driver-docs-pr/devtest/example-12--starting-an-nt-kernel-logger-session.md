---
title: 示例 12 启动 NT 内核记录器会话
description: 示例 12 启动 NT 内核记录器会话
ms.assetid: ce795cd3-4d95-49a1-a8b7-a32c69c776dd
keywords:
- 跟踪会话 WDK，NT 内核记录器
- NT 内核记录器跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f0c75886d6b984d0d794f3ed4087d09302e3c3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344722"
---
# <a name="example-12-starting-an-nt-kernel-logger-session"></a>示例 12：启动 NT 内核记录器会话


## <span id="ddk_starting_an_nt_kernel_logger_session_tools"></span><span id="DDK_STARTING_AN_NT_KERNEL_LOGGER_SESSION_TOOLS"></span>


以下命令启动的 NT 内核记录器跟踪会话。 由于 NT 内核记录器跟踪会话是默认值，因此不不需要任何其他参数。

```
tracelog -start
```

默认情况下，进程、 线程、 磁盘和 TCP/IP 跟踪事件。 若要替代默认值，可以使用设计为 NT 内核记录器会话的参数。

下面的命令使用 **-nothread**参数来关闭线程事件的跟踪 **-hf**参数，以跟踪硬页面错误和**cm**参数跟踪注册表事件。 此示例还使用可选 **-ft**参数，可以使用任何跟踪会话，将刷新缓冲区按固定的时间间隔此外到缓冲区已满时，会发生自动刷新。

```
tracelog -start -nothread -hf -cm -ft 2
```

此外可以使用 NT 内核记录器实时跟踪会话。 以下命令使用 NT 内核记录器启动实时跟踪会话。 同样，如上一示例中，可以省略会话名称，因为是默认的"NT 内核记录器"。

```
tracelog -start -rt
```

对于实时跟踪会话，除了自定义缓冲区和计时器分辨率的参数外，还可以使用自定义的 NT 内核记录器参数。

若要设置格式并显示此会话中的跟踪消息，请使用 Tracefmt。 下面的命令在命令提示符窗口中显示来自 NT 内核记录器会话的跟踪消息。 有关详细信息，请参阅[Tracefmt](tracefmt.md)。

```
tracefmt -rt -display
```

 

 






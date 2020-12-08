---
title: 示例11启动专用跟踪会话
description: 示例11启动专用跟踪会话
keywords:
- 跟踪会话 WDK，专用
- 专用跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71de3a6ec3f28252aa7f6a9eb17af564246d731a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817484"
---
# <a name="example-11-starting-a-private-trace-session"></a>示例 11：启动专用跟踪会话


## <span id="ddk_starting_a_private_trace_session_tools"></span><span id="DDK_STARTING_A_PRIVATE_TRACE_SESSION_TOOLS"></span>


下面的命令启动检测进行跟踪的用户模式应用程序的专用跟踪会话。

```
tracelog -start MyTrace -guid MyProvider.guid -um
```

您可以使用相同的参数自定义要用于标准跟踪会话的专用跟踪会话，但不能对专用跟踪会话进行实时跟踪。

**堆内存处理记录器。** 下面的命令启动一个专用会话，用于跟踪进程中的堆内存事件。 它适用于任何用户模式进程，甚至是未进行跟踪分析的进程。

由于此功能使用内置于 Windows 中的提供程序，因此此命令将使用正在跟踪的进程 ID) 指定进程 (，而不是使用正在生成跟踪消息的 GUID) 的访问 (接口。

此命令使用 **-um** 参数指定专用 (用户模式) trace 会话，并使用 **-堆** 参数指定堆内存跟踪。 它使用 **-pid** 参数指定要跟踪的进程的进程 ID。 在这种情况下，该命令包含一个 ID 为 **7008** 的进程。

该命令还使用可选的 **-f** 参数指定跟踪日志文件。 包含 **-f** 参数是为了提醒你可以使用大多数其他 Tracelog 参数自定义跟踪会话。

```
tracelog -start MyTrace -um -heap -pids 1 7008 -f testtrace.etl
```

**临界区进程记录器。** 下面的命令启动一个关键部分记录器，该事件记录进程中的关键部分事件。 此命令使用提供程序 (由 Windows 中包含的 GUID、CritsecGUID) 标识，因此它可以在任何用户模式进程上使用，即使不是为跟踪进行检测也是如此。

除了使用 **-critsec** 参数而不是 **-堆** 参数外，命令语法与堆内存进程记录器的语法相同。

在此示例中，该命令在两个相关进程上启动关键部分进程记录器。 因此， *\# pid* 变量的值为 **2**，并列出进程 id **4806** 和 **5164** 。

```
tracelog -start MyTrace -um -critsec -pids 2 4806 5164 -f testtrace.etl
```

 

 






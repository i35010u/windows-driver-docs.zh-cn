---
title: 示例 11 启动专用跟踪会话
description: 示例 11 启动专用跟踪会话
ms.assetid: e1826811-cb1c-400f-a3e1-aaa6ae83ef42
keywords:
- 跟踪会话 WDK，private
- 专用跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3915b51b215cb87742de5928065d1bf02e28aad4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540543"
---
# <a name="example-11-starting-a-private-trace-session"></a>示例 11:启动专用跟踪会话


## <span id="ddk_starting_a_private_trace_session_tools"></span><span id="DDK_STARTING_A_PRIVATE_TRACE_SESSION_TOOLS"></span>


以下命令启动跟踪检测到的用户模式应用程序的专用跟踪会话。

```
tracelog -start MyTrace -guid MyProvider.guid -um
```

可以使用相同的参数可以自定义标准跟踪会话，将使用的专用跟踪会话，但不能执行的专用跟踪会话的实时跟踪。

**堆内存过程记录器。** 以下命令启动隐私会话的跟踪过程中的堆内存事件。 它适用于任何用户模式进程，甚至是未检测的跟踪的一个。

由于此功能使用内置于 Windows 的提供程序，此命令指定正在跟踪，不使用的提供程序 （GUID） 生成的跟踪消息的进程 （使用进程 ID）...

此命令使用 **-um**参数来指定 （用户模式） 的专用跟踪会话并 **-堆**参数来指定堆内存跟踪。 它使用 **-pid**参数来指定要跟踪进程的进程 ID。 在这种情况下，该命令包含一个进程 id **7008**。

该命令还使用可选 **-f**参数来指定跟踪日志文件。 **-F**参数是包括在内，以提醒您，您可以使用大多数其他 Tracelog 参数以自定义跟踪会话。

```
tracelog -start MyTrace -um -heap -pids 1 7008 -f testtrace.etl
```

**关键部分过程记录器。** 以下命令启动一个临界区记录器，跟踪过程中的关键部分事件的专用会话。 此命令使用 （由 GUID CritsecGUID 标识） 的提供程序包含在 Windows 中，因此，但可用于任何用户模式进程，甚至是未检测的跟踪的一个。

命令语法等同于堆内存的进程记录器，只不过它使用 **-critsec**参数而不是 **-堆**参数。

在此示例中，该命令在两个相关进程启动关键部分过程记录器。 因此，值 *\#Pid*变量是**2**，并同时处理 Id **4806**并**5164**列出。

```
tracelog -start MyTrace -um -critsec -pids 2 4806 5164 -f testtrace.etl
```

 

 






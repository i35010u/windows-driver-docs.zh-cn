---
title: 示例9自定义跟踪日志文件
description: 示例9自定义跟踪日志文件
keywords:
- 跟踪日志 WDK
- 记录 WDK 跟踪
- 自定义跟踪日志 WDK
- 事件跟踪日志 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d59112a838ad3678bdc8f4567fba62f2711daa8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804267"
---
# <a name="example-9-customizing-the-trace-log-file"></a>示例 9：自定义跟踪日志文件


## <span id="ddk_customizing_the_trace_log_file_tools"></span><span id="DDK_CUSTOMIZING_THE_TRACE_LOG_FILE_TOOLS"></span>


此示例中的命令演示了用于自定义 Tracelog 生成的事件跟踪日志文件的不同方法。

**循环文件。** 以下命令使用循环日志文件启动跟踪日志会话。 它使用 **-cir** 参数指定最大大小为 2 MB 的循环日志文件。

如果省略了 "最大文件大小" 值 (在本例中为 **2**) ，Tracelog 将忽略参数，并启动具有顺序跟踪日志文件的会话。

```
tracelog -start MyTrace -guid MyProvider.guid -f testtrace.etl -cir 2
```

**预分配文件。** 以下命令使用预分配的文件启动跟踪日志会话。 在这种情况下，该文件已预分配，以确保在启动跟踪会话之前可以容纳其大大小。

此命令使用 **-seq** 参数指定最大文件大小为 128 MB 的顺序事件跟踪日志文件，并使用 **-prealloc** 参数来请求预分配文件。 顺序文件是默认值，但 **-seq** 参数用于指定可分配文件所需的最大文件大小。 如果首选循环文件，则 **-cir** 参数还可用于指定 **-prealloc** 的最大文件大小。

```
tracelog -start MyTrace -guid MyProvider.guid -f testtrace.etl -seq 128 -prealloc
```

**多个文件。** 下面的命令启动跟踪日志会话，该会话生成一系列较小的顺序事件跟踪日志文件，而不是一个大文件。

此命令使用 **-newfile** 参数，最大文件大小值为1，以便在当前日志文件达到 1 MB 时启动新的跟踪日志文件。 而且， **-f** 参数指定的文件名包含字符 **% d**，在使用 **-newfile** 时需要用到。 系统在创建每个文件时，将为 **% d** 替换一个文件计数器值。

```
tracelog -start MyTrace −guid MyProvider.guid -f testtrace%d.etl -newfile 1
```

生成的 1 MB 文件按创建顺序进行编号，例如 testtrace1。

 

 






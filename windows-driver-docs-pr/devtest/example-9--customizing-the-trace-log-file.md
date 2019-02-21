---
title: 示例 9 自定义跟踪日志文件
description: 示例 9 自定义跟踪日志文件
ms.assetid: b65b4d15-f058-425a-b2b2-b040265d48ac
keywords:
- 跟踪日志 WDK
- 日志 WDK 跟踪
- 自定义跟踪记录 WDK
- 事件跟踪日志 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eacb0221c65ec0afd4ce56364612bed3fd9aba0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521366"
---
# <a name="example-9-customizing-the-trace-log-file"></a>示例 9:自定义跟踪日志文件


## <span id="ddk_customizing_the_trace_log_file_tools"></span><span id="DDK_CUSTOMIZING_THE_TRACE_LOG_FILE_TOOLS"></span>


在此示例命令演示了用于自定义生成跟踪日志的事件跟踪日志文件的不同方法。

**循环文件。** 以下命令启动与循环日志文件跟踪日志会话。 它使用 **-cir**参数来指定具有的最大大小为 2 MB 的循环日志文件。

如果省略的最大文件大小值 (在这种情况下， **2**)，跟踪日志将忽略该参数，并与顺序跟踪日志文件启动会话。

```
tracelog -start MyTrace -guid MyProvider.guid -f testtrace.etl -cir 2
```

**预分配的文件。** 以下命令启动与预分配文件跟踪日志会话。 在这种情况下，该文件已预先分配以确保跟踪会话开始前，无法容纳其尺寸大。

此命令使用 **-seq**参数来指定顺序事件跟踪日志文件具有的最大文件大小为 128 MB，并且它使用 **-prealloc**参数来请求预分配的文件。 顺序文件是默认值，但 **-seq**参数用于指定最大文件大小，所需的预分配文件。 **-Cir**参数还可用于指定的最大文件大小 **-prealloc**，如果循环文件是首选。

```
tracelog -start MyTrace -guid MyProvider.guid -f testtrace.etl -seq 128 -prealloc
```

**多个文件。** 以下命令启动生成一系列较小的顺序事件跟踪日志文件，而不是一个大型文件的跟踪日志会话。

该命令使用 **-newfile**参数 1 以启动新的跟踪日志文件，只要当前日志文件达到 1 MB 的最大文件大小值。 此外，通过指定的文件名 **-f**参数包含的字符 **%d**，如使用时是必需 **-newfile**。 系统将为文件计数器值替换 **%d**时它会创建每个文件。

```
tracelog -start MyTrace −guid MyProvider.guid -f testtrace%d.etl -newfile 1
```

生成的 1MB 文件创建它们，例如 testtrace1.etl 的顺序进行编号。

 

 






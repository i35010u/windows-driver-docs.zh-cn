---
title: 如何实现从头文件生成跟踪消息
description: 如何实现从头文件生成跟踪消息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ea4dc509ab08fb1e64e4374202fb0536b9c8e92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799777"
---
# <a name="how-do-i-generate-trace-messages-from-a-header-file"></a>如何从标头文件生成跟踪消息？


若要从文件扩展名不是 .c、c + +、.cpp 和 .cxx 的源文件生成跟踪消息，请将 **-ext** 参数添加到运行 \_ 的 WPP 宏，该宏调用 Windows 软件跟踪预处理器。

例如，若要从 .c 和 .h 文件生成跟踪，请使用以下语句：

```
RUN_WPP=$(SOURCES) -km -ext:.c.h
```
确保 tracewpp 需要扫描的 .h 文件包含在中 `$(SOURCES)` ，或者在命令行上添加它们。  
例如：

```
RUN_WPP=$(SOURCES) tracedrv.h -km -ext:.c.h
```
不要 *包含使用* -scan：选项指定的 .h 文件作为配置数据文件，例如 `trace.h` 。

**-Ext** 参数指定 WPP 识别为源文件的文件类型。 WPP 将忽略具有不同文件扩展名的文件。 默认情况下，WPP 仅识别 .c、c + +、.cpp 和 .cxx 文件。

在 Windows Vista 之前的 Windows 版本中，由于此参数的值区分大小写，因此必须列出所有事例。 例如：

```
RUN_WPP=$(SOURCES) -km -ext:.c.C.h.H
```

此外，如果头文件与另一个源文件同名，请将 **-preserveext** 参数添加到 RUN \_ WPP 宏。 例如：

```
RUN_WPP=$(SOURCES) -km -ext:.c.C.h.H  -preserveext:.c.h
```

**-Preserveext** 参数将在创建 [跟踪消息标头](trace-message-header-file.md)的名称时保留指定的文件扩展名， ( tmh) 文件。 此参数可防止 WPP 创建具有相同名称的多个 TMH 文件。 默认情况下，WPP 仅使用 tmh 文件扩展名，例如 tracedrv. tmh。 对于 **-preserveext** 参数，文件将改为 tracedrv tmh 和 tracedrv。

有关运行 WPP 的可选参数的完整列表 \_ ，请参阅 [WPP 预处理器](wpp-preprocessor.md)。

 

 






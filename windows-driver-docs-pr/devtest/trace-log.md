---
title: 跟踪日志
description: 跟踪日志
keywords:
- 事件跟踪日志 WDK
- 日志文件 WDK 跟踪
- .etl 文件
- etl 文件
- 跟踪日志 WDK
- 存储跟踪消息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37201b304a4e3b008453005b60f04cecddad7d65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830133"
---
# <a name="trace-log"></a>跟踪日志


## <span id="ddk_trace_log_tools"></span><span id="DDK_TRACE_LOG_TOOLS"></span>


事件跟踪日志 ( .etl) 文件（也称为 *跟踪日志*）存储在一个或多个 [跟踪会话](trace-session.md)过程中生成的跟踪消息。

系统首先存储跟踪 [提供程序](trace-provider.md) 在跟踪会话缓冲区中生成的跟踪消息，然后将它们直接传递给 [跟踪使用者](trace-consumer.md) 或将它们写入跟踪日志。

由于这些消息会占用大量的磁盘空间，因此跟踪日志以压缩的二进制格式存储它们。 若要读取消息，跟踪使用者使用跟踪提供程序提供的信息 ([**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏) 中的 "*格式字符串*" 参数，以便对消息进行分析和格式设置，使其可读。 跟踪使用者可以在 [PDB 符号文件](pdb-symbol-files.md) 或提供程序的 [跟踪消息格式文件](trace-message-format-file.md) 中找到此信息。

 


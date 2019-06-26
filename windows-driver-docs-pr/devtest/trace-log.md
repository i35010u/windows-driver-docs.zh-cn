---
title: 跟踪日志
description: 跟踪日志
ms.assetid: c15fcfec-b584-4cb8-bc48-9ff122f5a8fc
keywords:
- 事件跟踪日志 WDK
- 日志文件 WDK 跟踪
- .etl 文件
- etl 文件
- 跟踪日志 WDK
- 存储跟踪消息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a6aabdf804d313c7def6a33ae4c960a4e44802f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380248"
---
# <a name="trace-log"></a>跟踪日志


## <span id="ddk_trace_log_tools"></span><span id="DDK_TRACE_LOG_TOOLS"></span>


事件跟踪日志 (.etl) 文件，也称为*跟踪日志*，将存储在一个或多个过程中生成的跟踪消息[跟踪会话](trace-session.md)。

系统首先将存储在跟踪消息[跟踪提供程序](trace-provider.md)跟踪会话缓冲区中生成并直接传递它们[跟踪使用者](trace-consumer.md)或将其写入到跟踪日志。

因为消息可以占用大量磁盘空间，跟踪日志会将其存储在压缩的二进制格式。 若要读取的消息，跟踪使用者使用提供的跟踪提供程序信息 ( *FormatString*中的参数[ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏) 分析和格式设置消息，以便它们是可读。 跟踪使用者可以找到此信息在[PDB 符号文件](pdb-symbol-files.md)或[跟踪消息格式文件](trace-message-format-file.md)提供程序。

 

 






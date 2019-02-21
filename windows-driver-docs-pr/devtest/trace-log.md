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
ms.openlocfilehash: e907f0f2082e4b0ff73c73336306f4eb435d5629
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545002"
---
# <a name="trace-log"></a>跟踪日志


## <span id="ddk_trace_log_tools"></span><span id="DDK_TRACE_LOG_TOOLS"></span>


事件跟踪日志 (.etl) 文件，也称为*跟踪日志*，将存储在一个或多个过程中生成的跟踪消息[跟踪会话](trace-session.md)。

系统首先将存储在跟踪消息[跟踪提供程序](trace-provider.md)跟踪会话缓冲区中生成并直接传递它们[跟踪使用者](trace-consumer.md)或将其写入到跟踪日志。

因为消息可以占用大量磁盘空间，跟踪日志会将其存储在压缩的二进制格式。 若要读取的消息，跟踪使用者使用提供的跟踪提供程序信息 ( *FormatString*中的参数[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)宏) 分析和格式设置消息，以便它们是可读。 跟踪使用者可以找到此信息在[PDB 符号文件](pdb-symbol-files.md)或[跟踪消息格式文件](trace-message-format-file.md)提供程序。

 

 






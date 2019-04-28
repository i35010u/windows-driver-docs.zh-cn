---
title: 显示跟踪日志
description: 显示跟踪日志
ms.assetid: c60c801a-6128-43d6-a435-4537c597177f
keywords:
- 跟踪日志 WDK TraceView，显示
- TraceView WDK，显示日志
- 显示跟踪日志
- 日志文件 WDK TraceView，显示
- 事件跟踪日志 WDK
- .etl 文件
- etl 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3687f2b7aaa26d058684d92ffa006113ddeb5e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348319"
---
# <a name="displaying-a-trace-log"></a>显示跟踪日志


可以使用 TraceView 要显示的任何内容[事件跟踪日志 (.etl) 文件](trace-level.md)(也称为*跟踪日志*)，包括使用 TraceView 没有生成的事件跟踪日志文件。

所有需要显示跟踪日志格式设置信息，可以通过定位提供给 TraceView [PDB 符号文件](pdb-symbol-files.md)(.pdb)[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)，或 TMF 文件的路径用于跟踪消息中。

在查看跟踪日志时，可以分组和取消分组跟踪日志、 生成新的跟踪日志文件，并复制用于以其他格式显示的跟踪消息。

本部分包括：

[显示使用 PDB 文件跟踪日志](displaying-a-trace-log-with-a-pdb-file.md)

[显示与 TMF 文件跟踪日志](displaying-a-trace-log-with-a-tmf-file.md)

[设置跟踪日志选项](setting-trace-log-options.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

TraceView 需要 PDB 文件、 TMF 文件或 TMF 目录以显示跟踪日志的内容。 TraceView 不使用 %跟踪\_格式\_搜索\_PATH %环境变量。

跟踪会话名称不会保存在事件跟踪日志 (.etl) 文件，或在 TraceView 输出文件或摘要文件。 当您使用 TraceView 显示跟踪日志时，它使用默认的会话名称，**LogSession * * * N*，作为跟踪会话的名称 (其中*N*是一个从零开始的整数，它表示的顺序创建会话）。

 

 






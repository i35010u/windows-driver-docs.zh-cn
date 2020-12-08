---
title: 显示跟踪日志
description: 显示跟踪日志
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
ms.openlocfilehash: 3c3919bda7c14e128cfda46aeea279b5ff9915f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839017"
---
# <a name="displaying-a-trace-log"></a>显示跟踪日志


你可以使用 TraceView 来显示任何 [事件跟踪日志 ( .etl) 文件](trace-level.md) 的内容 (也称为 *跟踪日志*) ，包括未使用 TraceView 生成的事件跟踪日志文件。

显示跟踪日志所需的所有内容都是格式设置信息，你可以通过 () 中找到 [pdb 符号文件](pdb-symbol-files.md) 、 [跟踪消息格式 ( tmf) 文件](trace-message-format-file.md)或跟踪消息的 tmf 文件的路径来向 TraceView 提供这些信息。

查看跟踪日志时，您可以对跟踪日志进行分组和取消分组，生成新的跟踪日志文件，并复制跟踪消息以便以其他格式显示。

本节包括：

[使用 PDB 文件显示跟踪日志](displaying-a-trace-log-with-a-pdb-file.md)

[显示包含 TMF 文件的跟踪日志](displaying-a-trace-log-with-a-tmf-file.md)

[设置跟踪日志选项](setting-trace-log-options.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

TraceView 需要 PDB 文件、TMF 文件或 TMF 目录来显示跟踪日志的内容。 TraceView 不使用% 跟踪 \_ 格式 \_ 搜索 \_ 路径% 环境变量。

跟踪会话名称不会保存在事件跟踪日志 ( .etl) 文件中，也不会保存在 TraceView 输出文件或摘要文件中。 使用 TraceView 显示跟踪日志时，它将使用默认会话名称 **LogSession**_N_ 作为跟踪 (会话的名称，其中 *N* 是一个从零开始的整数，该整数表示) 创建会话的顺序。

 

 






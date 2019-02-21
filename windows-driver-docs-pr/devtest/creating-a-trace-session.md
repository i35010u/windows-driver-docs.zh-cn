---
title: 创建跟踪会话
description: 创建跟踪会话
ms.assetid: 26f75b02-d830-4e3c-bbc9-03144d194e05
keywords:
- 实时跟踪会话 WDK
- 跟踪日志会话 WDK
- TraceView WDK，创建的会话
- 跟踪会话 WDK，创建
- 会话 WDK 软件跟踪
- 跟踪 WDK、 会话创建的软件
- 跟踪 WDK、 会话创建
- 跟踪日志 WDK TraceView 会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b16a8986a75df60548ef75b1d9cdf7efc2f18ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527116"
---
# <a name="creating-a-trace-session"></a>创建跟踪会话


## <span id="ddk_creating_a_real_time_trace_session_tools"></span><span id="DDK_CREATING_A_REAL_TIME_TRACE_SESSION_TOOLS"></span>


本部分介绍如何使用 TraceView 创建实时跟踪会话或跟踪日志会话。

当您*创建*[跟踪会话](trace-session.md)，TraceView 配置和启动跟踪会话，并使[跟踪提供程序](trace-provider.md)指定，如在提供程序事件跟踪进行检测的驱动程序。

TraceView 使用向导页以指导你完成创建跟踪会话的步骤。

TraceView 要求创建跟踪会话时指定至少一个跟踪提供程序。 提供程序类型和文件可确定用于创建跟踪会话的方法。

本部分包括：

[使用 PDB 文件创建跟踪会话](creating-a-trace-session-with-a-pdb-file.md)

[使用 CTL 文件创建跟踪会话](creating-a-trace-session-with-a-ctl-file.md)

[使用控件的 GUID 创建跟踪会话](creating-a-trace-session-with-a-control-guid.md)

[为注册的提供程序创建跟踪会话](creating-a-trace-session-for-a-registered-provider.md)

[NT 内核记录器跟踪会话的创建](creating-an-nt-kernel-logger-trace-session.md)

[加入跟踪会话](joining-a-trace-session.md)

[删除跟踪提供程序](removing-a-trace-provider.md)

[设置基本跟踪会话选项](setting-basic-trace-session-options.md)

[选择标志和级别](selecting-flags-and-levels.md)

[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

需要 TraceView [PDB 符号文件](pdb-symbol-files.md)即[跟踪消息格式 (TMF) 文件](trace-message-format-file.md)，或 TMF 目录创建跟踪会话时。 TraceView 不使用 %跟踪\_格式\_搜索\_PATH %环境变量。

当使用 TraceView 窗口来创建跟踪会话，跟踪会话运行，只要该窗口保持打开状态。 无法关闭窗口和保留正在运行的会话。 若要启动独立于 TraceView 窗口运行跟踪会话，请使用[TraceView 命令行界面](traceview-command-line-interface.md)。

 

 






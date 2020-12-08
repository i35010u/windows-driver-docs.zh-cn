---
title: 创建跟踪会话
description: 创建跟踪会话
keywords:
- 实时跟踪会话 WDK
- 跟踪日志会话 WDK
- TraceView WDK，创建会话
- 跟踪会话 WDK，创建
- 会话 WDK 软件跟踪
- 软件跟踪 WDK，会话创建
- 跟踪 WDK，会话创建
- 跟踪日志 WDK TraceView，会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 498759d1e555d39234329fc81afe2388fb160731
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799779"
---
# <a name="creating-a-trace-session"></a>创建跟踪会话


## <span id="ddk_creating_a_real_time_trace_session_tools"></span><span id="DDK_CREATING_A_REAL_TIME_TRACE_SESSION_TOOLS"></span>


本部分介绍如何使用 TraceView 创建实时跟踪会话或跟踪日志会话。

当你 *创建*[跟踪会话](trace-session.md)时，TraceView 将配置并启动跟踪会话，并启用指定的 [跟踪提供程序](trace-provider.md)，如检测到事件跟踪的驱动程序中的提供程序。

TraceView 使用向导页指导您完成创建跟踪会话的步骤。

TraceView 要求在创建跟踪会话时至少指定一个跟踪提供程序。 提供程序类型和可用的文件决定了创建跟踪会话时使用的方法。

本节包括：

[使用 PDB 文件创建跟踪会话](creating-a-trace-session-with-a-pdb-file.md)

[使用 CTL 文件创建跟踪会话](creating-a-trace-session-with-a-ctl-file.md)

[使用控件 GUID 创建跟踪会话](creating-a-trace-session-with-a-control-guid.md)

[为注册的提供程序创建跟踪会话](creating-a-trace-session-for-a-registered-provider.md)

[创建 NT 内核记录器跟踪会话](creating-an-nt-kernel-logger-trace-session.md)

[加入跟踪会话](joining-a-trace-session.md)

[删除跟踪提供程序](removing-a-trace-provider.md)

[设置基本跟踪会话选项](setting-basic-trace-session-options.md)

[选择标志和级别](selecting-flags-and-levels.md)

[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

创建跟踪会话时，TraceView 需要 [PDB 符号文件](pdb-symbol-files.md)、 [跟踪消息格式 (TMF) 文件](trace-message-format-file.md)或 TMF 目录。 TraceView 不使用% 跟踪 \_ 格式 \_ 搜索 \_ 路径% 环境变量。

当您使用 TraceView 窗口创建跟踪会话时，只要窗口保持打开状态，trace 会话就会运行。 您无法关闭窗口并使会话保持运行状态。 若要启动独立于 TraceView 窗口运行的跟踪会话，请使用 [TraceView 命令行接口](traceview-command-line-interface.md)。

 

 






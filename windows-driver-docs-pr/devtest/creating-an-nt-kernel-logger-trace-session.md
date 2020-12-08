---
title: 创建 NT 内核记录器跟踪会话
description: 创建 NT 内核记录器跟踪会话
keywords:
- 跟踪会话 WDK，NT 内核记录器
- NT 内核记录器跟踪会话 WDK
- Windows 内核跟踪提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8dba0c78ce8a9549c47438d3cb9795c08fb74aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818601"
---
# <a name="creating-an-nt-kernel-logger-trace-session"></a>创建 NT 内核记录器跟踪会话

## <span id="ddk_create_a_real_time_nt_kernel_logger_trace_session_tools"></span><span id="DDK_CREATE_A_REAL_TIME_NT_KERNEL_LOGGER_TRACE_SESSION_TOOLS"></span>

你可以使用 TraceView 来创建 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)，这是 windows 中内置的跟踪会话，用于记录 windows 内核生成的事件。

创建 NT 内核记录器跟踪会话时，可以选择一类系统事件，如 "进程"。 TraceView 配置跟踪会话以记录该类别中的所有系统事件。

### <a name="span-idto_create_an_nt_kernel_logger_trace_sessionspanspan-idto_create_an_nt_kernel_logger_trace_sessionspanto-create-an-nt-kernel-logger-trace-session"></a><span id="to_create_an_nt_kernel_logger_trace_session"></span><span id="TO_CREATE_AN_NT_KERNEL_LOGGER_TRACE_SESSION"></span>创建 NT 内核记录器跟踪会话

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  在 " **文件** " 菜单上，单击 " **创建新的日志会话**"。

3.  单击 **“添加提供程序”**。

4.  单击 " **内核记录器**"，选择一个或多个标识 NT 内核记录器会话事件类型的复选框，然后单击 **"确定"**。

5.  在 " **打开** " 对话框中，找到 "tmf"，跟踪消息格式 ("tmf" 为系统事件) 文件。 Tmf 包含在 WDK 的 "工具" \\ 跟踪子目录中。

6.  若要添加任何类型的其他提供程序，请单击 " **添加提供程序**"。 此步骤是可选的。

7.  单击 **“下一步”** 。

8.  如果需要，请[设置基本跟踪会话选项](setting-basic-trace-session-options.md)。

9.  如果需要，请[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

10. 单击“完成”。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

"NT 内核记录器跟踪会话" 显示在 " **指定提供程序选择** " 对话框的列表中作为 "Windows 内核跟踪"。 您可以使用 "**提供程序控制 GUID 设置**" 对话框中的 "**命名提供程序选择**" 对话框或 "**内核记录器**" 选项来创建 NT 内核记录器跟踪会话。 但是，只允许 " **提供程序控件 GUID 设置** " 对话框选择要跟踪的内核组件。 有关使用 " **命名提供程序选择** " 对话框的详细信息，请参阅 [为注册的提供程序创建跟踪会话](creating-a-trace-session-for-a-registered-provider.md)。

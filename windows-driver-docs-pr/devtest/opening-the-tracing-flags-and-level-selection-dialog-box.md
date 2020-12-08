---
title: 打开跟踪标志和级别选择对话框
description: 打开跟踪标志和级别选择对话框
keywords:
- 跟踪标志 WDK
- 标志 WDK 软件跟踪
- 跟踪级别 WDK
- 级别 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5918ada2c5243cda1ac43b2484d9c36092435ac6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840799"
---
# <a name="opening-the-tracing-flags-and-level-selection-dialog-box"></a>打开跟踪标志和级别选择对话框


您可以使用 " **跟踪标志和级别选择** " 对话框来选择和更改在创建会话时和会话运行时的提供程序的标志和级别。

### <a name="span-idwhile_creating_a_trace_sessionspanspan-idwhile_creating_a_trace_sessionspanwhile-creating-a-trace-session"></a><span id="while_creating_a_trace_session"></span><span id="WHILE_CREATING_A_TRACE_SESSION"></span>创建跟踪会话时

1.  [启动 TraceView。](starting-and-exiting-traceview.md)

2.  在 " **文件** " 菜单上，单击 " **创建新的日志会话**"。

3.  单击 " **添加提供程序** " 并添加提供程序。

4.  添加其他提供程序（如果需要）。

5.  单击 **“下一步”** 。

6.  在 " **日志会话选项** " 页面上，单击 " **设置标志和级别** " 按钮。

### <a name="span-idwhile_a_trace_session_is_runningspanspan-idwhile_a_trace_session_is_runningspanwhile-a-trace-session-is-running"></a><span id="while_a_trace_session_is_running"></span><span id="WHILE_A_TRACE_SESSION_IS_RUNNING"></span>跟踪会话正在运行时

1.  在 " [跟踪会话" 列表](trace-session-list.md)中，找到跟踪会话的行。

2.  找到该行的 " **标志** " 或 " **级别** " 列，然后单击 " **设置** " 值。  (在使用 PDB 文件识别会话提供程序时 **设置** 值。 ) 

3.  单击 " **设置** " 将打开 " **跟踪标志和级别选择** " 对话框。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

仅当 TraceView 可以找到提供程序的 [PDB 符号文件](pdb-symbol-files.md)或在 TMF 路径中 ( 找到该提供程序的 [) 文件](trace-message-control-file.md)时，才会启用 "**设置标志和级别**" 选项， (通过使用 "**设置 TMF 搜索路径**" 选项) 指定。

 

 






---
title: 打开跟踪标志和级别所选内容对话框
description: 打开跟踪标志和级别所选内容对话框
ms.assetid: f6ee808e-ea29-492b-b161-0a3b57140214
keywords:
- 跟踪标志 WDK
- 标志 WDK 软件跟踪
- 跟踪级别 WDK
- 级别 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea90faac2f86afc3a68b03b0ab21f6f9feb634bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545613"
---
# <a name="opening-the-tracing-flags-and-level-selection-dialog-box"></a>打开跟踪标志和级别所选内容对话框


可以使用**跟踪标志和级别选择**对话框来选择和更改的标志和提供程序的级别时创建会话和而会话正在运行。

### <a name="span-idwhilecreatingatracesessionspanspan-idwhilecreatingatracesessionspanwhile-creating-a-trace-session"></a><span id="while_creating_a_trace_session"></span><span id="WHILE_CREATING_A_TRACE_SESSION"></span>创建跟踪会话时

1.  [启动 TraceView。](starting-and-exiting-traceview.md)

2.  上**文件**菜单上，单击**新建日志会话**。

3.  单击**添加提供程序**和添加提供程序。

4.  如果需要，添加其他提供程序...

5.  单击“下一步” 。

6.  上**日志会话选项**页上，单击**设置标志和级别**按钮。

### <a name="span-idwhileatracesessionisrunningspanspan-idwhileatracesessionisrunningspanwhile-a-trace-session-is-running"></a><span id="while_a_trace_session_is_running"></span><span id="WHILE_A_TRACE_SESSION_IS_RUNNING"></span>跟踪会话正在运行时

1.  在中[跟踪会话列表](trace-session-list.md)，用于跟踪会话中找到的行。

2.  找到**标志**或**级别**列的行，然后单击**设置**值。 (的值是**设置**时使用 PDB 文件来标识的会话提供程序。)

3.  单击**设置**会打开**跟踪标志和级别选择**对话框。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**设置标志和级别**TraceView 可以找到时，才启用选项[PDB 符号文件](pdb-symbol-files.md)提供程序或它可以找到[跟踪消息控件 (.tmc) 文件](trace-message-control-file.md)为TMF 路径中的提供程序 (通过使用指定**设置 TMF 搜索路径**选项)。

 

 






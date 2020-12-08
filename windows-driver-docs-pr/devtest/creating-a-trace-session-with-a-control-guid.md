---
title: 使用控制 GUID 创建跟踪会话
description: 使用控制 GUID 创建跟踪会话
keywords:
- 控制 Guid WDK
- Guid WDK 软件跟踪
- 标识符 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c870531f24b18b018fe1db7c3a9bc1a32c0db0c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792371"
---
# <a name="creating-a-trace-session-with-a-control-guid"></a>使用控制 GUID 创建跟踪会话


您可以通过键入或粘贴跟踪提供程序的 [控件 GUID](control-guid.md) 并为其消息查找 [跟踪消息格式 () 文件](trace-message-format-file.md) 来创建跟踪会话。

### <a name="span-idto_create_a_trace_session_by_typing_or_pasting_the_control_guidspanspan-idto_create_a_trace_session_by_typing_or_pasting_the_control_guidspanto-create-a-trace-session-by-typing-or-pasting-the-control-guid"></a><span id="to_create_a_trace_session_by_typing_or_pasting_the_control_guid"></span><span id="TO_CREATE_A_TRACE_SESSION_BY_TYPING_OR_PASTING_THE_CONTROL_GUID"></span>通过键入或粘贴控件 GUID 来创建跟踪会话

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  在 " **文件** " 菜单上，单击 " **创建新的日志会话**"。

3.  单击 **“添加提供程序”**。

4.  单击 " **手动输入的控件 guid** "，然后键入或粘贴控件 guid。

5.  执行下列操作之一：

6.  -   若要指定一个或多个 TMF 文件，请单击 " **选择 TMF 文件**"，单击 **"确定**"，再单击 " **添加**"，然后浏览到并从目录中选择一个或多个 TMF 文件。 若要从其他目录中选择 TMF 文件，请再次单击 " **添加** " 按钮。 否则，单击 " **完成**"。
    -   若要指示 TraceView 在指定目录中搜索 TMF 文件，请单击 " **设置 TMF 搜索路径**"，单击 **"确定**"，浏览到该目录，然后单击 **"确定"**。

7.  若要添加其他提供程序，请单击 " **添加提供程序**"。 此步骤是可选的。

8.  单击 **“下一步”** 。

9.  如果需要，请[选择 "标志" 和 "级别](selecting-flags-and-levels.md)"。

10. 如果需要，请[设置基本跟踪会话选项](setting-basic-trace-session-options.md)。

11. 如果需要，请[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

12. 单击“完成”。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

如果 TraceView 找不到跟踪提供程序的 TMF 文件，则它不会将跟踪提供程序添加到 " **创建新的日志会话** " 对话框的 "提供程序" 列表中，并且不会显示说明未添加提供程序的原因的消息。 如果提供程序未显示在提供程序列表中，请重新启动该过程，并使用 " **选择 TMF 文件** " 方法而不是 **设置 TMF 搜索路径**。 如果找不到该提供程序的 PDB 文件或 TMF 文件，则不能使用 TraceView 创建跟踪会话。

通过键入或粘贴控件 GUID 创建跟踪会话时，您可以使用 " **跟踪标志和级别选择** " 对话框 (仅当 TraceView 可以查找提供程序的 PDB 符号文件时，) [选择 "标记和级别](selecting-flags-and-levels.md) " 中所述的内容，或者可以在 TMF 路径中找到提供程序的 tmc) 文件， (使用 " ( 设置 TMF 搜索路径" 选项) 指定。

如果 TMC 文件不可用，则可以在 " **高级跟踪会话选项** " 对话框中手动设置跟踪标志和该提供程序的级别。 有关说明，请参阅 [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

有关指定 TMF 文件的信息，请参阅设置 TMF 搜索路径和选择 TMF 文件选项。

 

 






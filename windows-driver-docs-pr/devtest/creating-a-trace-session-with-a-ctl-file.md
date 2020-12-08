---
title: 使用 CTL 文件创建跟踪会话
description: 使用 CTL 文件创建跟踪会话
keywords:
- 控制 Guid WDK
- ctl 文件
- ctl 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ea13e10ecab3e89cd871b812b0781e5e91a0c40
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792369"
---
# <a name="creating-a-trace-session-with-a-ctl-file"></a>使用 CTL 文件创建跟踪会话


## <span id="ddk_create_a_trace_session_with_a_ctl_file_tools"></span><span id="DDK_CREATE_A_TRACE_SESSION_WITH_A_CTL_FILE_TOOLS"></span>


您可以通过为跟踪提供程序查找 [ ( 的控件 GUID) 文件](control-guid-file.md) ，并为其消息查找 [ () 文件的跟踪消息格式](trace-message-format-file.md) 来创建跟踪会话。

### <a name="span-idto_create_a_trace_session_with_a_ctl_filespanspan-idto_create_a_trace_session_with_a_ctl_filespanto-create-a-trace-session-with-a-ctl-file"></a><span id="to_create_a_trace_session_with_a_ctl_file"></span><span id="TO_CREATE_A_TRACE_SESSION_WITH_A_CTL_FILE"></span>使用 CTL 文件创建跟踪会话

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  在 " **文件** " 菜单上，单击 " **创建新的日志会话**"。

3.  单击 **“添加提供程序”**。

4.  单击 " **CTL (控件 guid) 文件**"，然后键入跟踪提供程序的 [控件 guid 文件](control-guid-file.md) 的路径;或者，单击省略号 **按钮 ()** 并导航到该文件。

5.  执行下列操作之一：
    -   若要指定一个或多个 TMF 文件，请单击 " **选择 TMF 文件**"，单击 **"确定**"，再单击 " **添加**"，然后浏览到并从目录中选择一个或多个 TMF 文件。 若要从其他目录中选择 TMF 文件，请再次单击 " **添加** " 按钮。 否则，单击 " **完成**"。
    -   若要指示 TraceView 在指定目录中搜索 TMF 文件，请单击 " **设置 TMF 搜索路径**"，单击 **"确定**"，浏览到该目录，然后单击 **"确定"**。

6.  若要添加其他提供程序，请单击 " **添加提供程序**"。 此步骤是可选的。

7.  单击 **“下一步”** 。

8.  如果需要，请[选择 "标志" 和 "级别](selecting-flags-and-levels.md)"。

9.  如果需要，请[设置基本跟踪会话选项](setting-basic-trace-session-options.md)。

10. 如果需要，请[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

11. 单击“完成”。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

如果 TraceView 找不到跟踪提供程序的 TMF 文件，则它不会将跟踪提供程序添加到 " **创建新的日志会话** " 对话框的 "提供程序" 列表中，并且不会显示说明未添加提供程序的原因的消息。 如果提供程序未显示在提供程序列表中，请重新启动该过程，并使用 " **选择 TMF 文件** " 方法而不是 **设置 TMF 搜索路径**。 如果找不到提供程序的 PDB 文件或 TMF 文件，则不能使用 TraceView 创建与提供程序的跟踪会话。

你可以将文件扩展名为 ". ctl" 的文件与 **ctl (CONTROL GUID) file** "选项一起使用。 TraceView 只要求文件是文本文件，每个控件 GUID 都出现在文件中的单独一行上，并且控件 GUID 是行中的第一个文本。 如果提交其他格式的文件，TraceView 将接受该文件，但不会启用未正确指定的提供程序。

控件 GUID 文件可以包含多个控制 Guid。 TraceView 启用所有控件 Guid 显示在文件中的提供程序。

使用控件 GUID 创建跟踪会话时，你可以使用 " **跟踪标志和级别选择** " 对话框 (仅当 TraceView 可以找到提供程序的 PDB 符号文件时，) [选择 "标记和级别](selecting-flags-and-levels.md) " 中所述的内容，或者在 TMF 路径中找到提供程序的跟踪消息控件 ( tmc) 文件 (。

如果 TMC 文件不可用，则可以在 " **高级跟踪会话选项** " 对话框中手动设置跟踪标志和该提供程序的级别。 有关说明，请参阅 [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

有关指定 TMF 文件的信息，请参阅选择 TMF 文件和设置 TMF 搜索路径。

 

 






---
title: 使用 CTL 文件创建跟踪会话
description: 使用 CTL 文件创建跟踪会话
ms.assetid: aa9aee7b-d0d2-44fe-a124-3594078a8e6c
keywords:
- 控件 Guid WDK
- .ctl 文件
- ctl 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bc6cf38da8435feff70cbd7a554dea11f496d00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563736"
---
# <a name="creating-a-trace-session-with-a-ctl-file"></a>使用 CTL 文件创建跟踪会话


## <span id="ddk_create_a_trace_session_with_a_ctl_file_tools"></span><span id="DDK_CREATE_A_TRACE_SESSION_WITH_A_CTL_FILE_TOOLS"></span>


可以通过定位创建跟踪会话[控制 GUID (.ctl) 文件](control-guid-file.md)跟踪提供程序和查找[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)其消息。

### <a name="span-idtocreateatracesessionwithactlfilespanspan-idtocreateatracesessionwithactlfilespanto-create-a-trace-session-with-a-ctl-file"></a><span id="to_create_a_trace_session_with_a_ctl_file"></span><span id="TO_CREATE_A_TRACE_SESSION_WITH_A_CTL_FILE"></span>若要使用 CTL 文件创建跟踪会话

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  上**文件**菜单上，单击**新建日志会话**。

3.  单击**添加提供程序**。

4.  单击**CTL (控制 GUID) 文件**，然后键入的路径[控制 GUID 文件](control-guid-file.md)跟踪提供程序; 或单击省略号按钮 (**...**) 并导航到该文件。

5.  执行下列操作之一：
    -   若要指定一个或多个 TMF 文件，请单击**选择 TMF 文件**，单击**确定**，单击**添加**，然后浏览到并从目录中选择一个或多个 TMF 文件。 若要从另一个目录中选择 TMF 文件，请单击**添加**按钮再次。 否则，请单击**完成**。
    -   若要指示 TraceView，搜索指定目录中 TMF 文件，请单击**设置 TMF 搜索路径**，单击**确定**，浏览到的目录，然后单击**确定**。

6.  若要添加其他提供程序，请单击**添加提供程序**。 此步骤可选。

7.  单击“下一步” 。

8.  [选择标志和级别](selecting-flags-and-levels.md)，如果所需的。

9.  [设置会话选项的基本跟踪](setting-basic-trace-session-options.md)，如果所需的。

10. [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)，如果所需的。

11. 单击 **“完成”**。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

如果 TraceView 找不到 TMF 文件跟踪提供程序，则不会添加跟踪提供程序的提供程序列表中向**新建日志会话**对话框中，它不显示一条消息，说明为何未添加提供程序。 如果提供程序不会出现在提供程序列表中，重新启动该过程并使用**选择 TMF 文件**方法而不是**设置 TMF 搜索路径**。 如果您找不到提供程序的 PDB 文件或 TMF 文件，则无法使用 TraceView 与提供程序创建跟踪会话。

具有".ctl"以外的文件扩展名的文件可用于**CTL (控制 GUID) 文件**选项。 TraceView 仅要求该文件的文本文件，每个控件 GUID 显示在单独的行在文件中，并且控件 GUID 是在行上的第一个文本。 如果提交具有不同格式的文件，TraceView 接受文件，但不会启用提供程序未正确指定。

控件 GUID 文件可以包含多个控件的 Guid。 TraceView 启用所有提供程序的控件显示在文件中的 Guid。

控件 GUID 与创建跟踪会话，可以使用**跟踪标志和级别选择**对话框 (中所述[选择标志和级别](selecting-flags-and-levels.md)) 仅当 TraceView 可以找到 PDB提供程序或它可以提供程序 （通过设置 TMF 搜索路径选项指定） 的 TMF 路径中找到跟踪消息控件 (.tmc) 文件的符号文件。

如果 TMC 文件不可用，则可以设置的跟踪标志和级别的提供程序中手动**高级跟踪会话选项**对话框。 有关说明，请参阅[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

有关指定 TMF 文件的信息，请参阅选择 TMF 文件和设置 TMF 搜索路径。

 

 






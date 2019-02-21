---
title: 控件 GUID 与创建跟踪会话
description: 控件 GUID 与创建跟踪会话
ms.assetid: a651ac6b-9ae0-46b0-8180-59d70ceb57fe
keywords:
- 控件 Guid WDK
- Guid WDK 软件跟踪
- 标识符 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16c40c4bbf3f20d82ba2269d5099e170d100635a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524827"
---
# <a name="creating-a-trace-session-with-a-control-guid"></a>控件 GUID 与创建跟踪会话


可以通过键入或粘贴创建跟踪会话[控制 GUID](control-guid.md)跟踪的提供程序和定位[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)为其消息。

### <a name="span-idtocreateatracesessionbytypingorpastingthecontrolguidspanspan-idtocreateatracesessionbytypingorpastingthecontrolguidspanto-create-a-trace-session-by-typing-or-pasting-the-control-guid"></a><span id="to_create_a_trace_session_by_typing_or_pasting_the_control_guid"></span><span id="TO_CREATE_A_TRACE_SESSION_BY_TYPING_OR_PASTING_THE_CONTROL_GUID"></span>若要通过键入或粘贴控件 GUID 创建跟踪会话

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  上**文件**菜单上，单击**新建日志会话**。

3.  单击**添加提供程序**。

4.  单击**手动输入控件 GUID**然后键入或粘贴控件的 GUID。

5.  执行下列操作之一：

6.  -   若要指定一个或多个 TMF 文件，请单击**选择 TMF 文件**，单击**确定**，单击**添加**，然后浏览到并从目录中选择一个或多个 TMF 文件。 若要从另一个目录中选择 TMF 文件，请单击**添加**按钮再次。 否则，请单击**完成**。
    -   若要指示 TraceView，搜索指定目录中 TMF 文件，请单击**设置 TMF 搜索路径**，单击**确定**，浏览到的目录，然后单击**确定**。

7.  若要添加其他提供程序，请单击**添加提供程序**。 此步骤可选。

8.  单击“下一步” 。

9.  [选择标志和级别](selecting-flags-and-levels.md)，如果所需的。

10. [设置会话选项的基本跟踪](setting-basic-trace-session-options.md)，如果所需的。

11. [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)，如果所需的。

12. 单击“完成” 。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

如果 TraceView 找不到 TMF 文件跟踪提供程序，则不会添加跟踪提供程序的提供程序列表中向**新建日志会话**对话框中，它不显示一条消息，说明为何未添加提供程序。 如果提供程序不会出现在提供程序列表中，重新启动该过程并使用**选择 TMF 文件**方法而不是**设置 TMF 搜索路径**。 如果您找不到提供程序的 PDB 文件或 TMF 文件，则无法使用 TraceView 创建跟踪会话。

通过键入或粘贴控件 GUID 创建跟踪会话，可以使用**跟踪标志和级别选择**对话框 (中所述[选择标志和级别](selecting-flags-and-levels.md)) 仅当 TraceView 可以提供程序或它可以找到跟踪消息控件 (.tmc) 文件提供程序 （通过设置 TMF 搜索路径选项指定） 的 TMF 路径中找到的 PDB 符号文件。

如果 TMC 文件不可用，则可以设置的跟踪标志和级别的提供程序中手动**高级跟踪会话选项**对话框。 有关说明，请参阅[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

有关指定 TMF 文件的信息，请参阅设置 TMF 搜索路径和选择 TMF 文件选项。

 

 






---
title: 为注册的提供程序创建跟踪会话
description: 为注册的提供程序创建跟踪会话
ms.assetid: 3013b5fa-5390-4d46-b138-4ddcda468ddf
keywords:
- 注册的提供程序 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9bd580f5251a74e34a74eee211cb3bbb3e2f9b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555672"
---
# <a name="creating-a-trace-session-for-a-registered-provider"></a>为注册的提供程序创建跟踪会话


## <span id="ddk_create_a_trace_session_for_a_registered_provider_tools"></span><span id="DDK_CREATE_A_TRACE_SESSION_FOR_A_REGISTERED_PROVIDER_TOOLS"></span>


若要监视的跟踪消息[注册的提供程序](registered-provider.md)，执行以下操作：

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  上**文件**菜单上，单击**新建日志会话**。

3.  单击**添加提供程序**。

4.  单击**名为提供程序**，然后单击省略号按钮 (**...**) 旁边**名为提供程序**文本框。

    在中**名为提供程序选择**对话框中，TraceView 显示系统中注册的提供程序。

5.  选择已注册的提供程序，然后依次**确定**。

6.  执行下列操作之一：
    -   若要指定一个或多个 TMF 文件，请单击**选择 TMF 文件**，单击**确定**，单击**添加**，然后浏览到并从目录中选择一个或多个 TMF 文件。 若要从另一个目录中选择 TMF 文件，请单击**添加**按钮再次。 否则，请单击**完成**。
    -   若要指示 TraceView，搜索指定目录中 TMF 文件，请单击**设置 TMF 搜索路径**，单击**确定**，浏览到的目录，然后单击**确定**。

7.  若要添加的任何类型的其他提供程序，请单击**添加提供程序**。 此步骤可选。

8.  单击“下一步” 。

9.  [设置会话选项的基本跟踪](setting-basic-trace-session-options.md)，如果所需的。

10. [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)，如果所需的。

11. 单击“完成” 。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

有关指定 TMF 文件的信息，请参阅选择 TMF 文件和设置 TMF 搜索路径。

若要注册的提供程序设置标志和级别，请参阅[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

命名的提供程序列表中显示的"Windows 内核跟踪"提供程序是更好地称为[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。 可以使用**名为提供程序选择**对话框中创建 NT 内核记录器跟踪会话，但此对话框不允许您选择要跟踪的内核组件。 相反，它将选择默认组件 （进程、 线程、 磁盘和网络）。 若要选择的跟踪组件，使用 NT 内核记录器跟踪会话的自定义的 TraceView 接口。

TMF 文件对于 Windows 内核跟踪，system.tmf，包含在 WDK 中。 单击**选择 TMF 文件**，单击**添加**，导航到\\工具\\跟踪\\i386 子目录中，然后选择 system.tmf。

有关详细信息，请参阅[NT 内核记录器跟踪会话的创建](creating-an-nt-kernel-logger-trace-session.md)。

 

 






---
title: 为已注册的提供程序创建跟踪会话
description: 为已注册的提供程序创建跟踪会话
keywords:
- 已注册的提供程序 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fc78feef1abc64ab9cc6fa28ab5a2d8ba44e7de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792383"
---
# <a name="creating-a-trace-session-for-a-registered-provider"></a>为已注册的提供程序创建跟踪会话


## <span id="ddk_create_a_trace_session_for_a_registered_provider_tools"></span><span id="DDK_CREATE_A_TRACE_SESSION_FOR_A_REGISTERED_PROVIDER_TOOLS"></span>


若要监视 [已注册提供程序](registered-provider.md)的跟踪消息，请执行以下操作：

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  在 " **文件** " 菜单上，单击 " **创建新的日志会话**"。

3.  单击 **“添加提供程序”**。

4.  单击 "**命名提供程序**"，然后单击 "**命名提供程序**" 文本框旁边的省略号 **按钮 (") "。**

    在 " **命名提供程序选择** " 对话框中，TraceView 显示系统中已注册的提供程序。

5.  选择已注册的提供程序，然后单击 **"确定"**。

6.  执行下列操作之一：
    -   若要指定一个或多个 TMF 文件，请单击 " **选择 TMF 文件**"，单击 **"确定**"，再单击 " **添加**"，然后浏览到并从目录中选择一个或多个 TMF 文件。 若要从其他目录中选择 TMF 文件，请再次单击 " **添加** " 按钮。 否则，单击 " **完成**"。
    -   若要指示 TraceView 在指定目录中搜索 TMF 文件，请单击 " **设置 TMF 搜索路径**"，单击 **"确定**"，浏览到该目录，然后单击 **"确定"**。

7.  若要添加任何类型的其他提供程序，请单击 " **添加提供程序**"。 此步骤是可选的。

8.  单击 **“下一步”** 。

9.  如果需要，请[设置基本跟踪会话选项](setting-basic-trace-session-options.md)。

10. 如果需要，请[设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

11. 单击“完成”。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

有关指定 TMF 文件的信息，请参阅选择 TMF 文件和设置 TMF 搜索路径。

若要为注册的提供程序设置标志和级别，请参阅 [设置高级跟踪会话选项](setting-advanced-trace-session-options.md)。

命名提供程序列表中显示的 "Windows 内核跟踪" 提供程序更好地称为 " [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)"。 您可以使用 " **命名提供程序选择** " 对话框创建 NT 内核记录器跟踪会话，但此对话框不允许您选择要跟踪的内核组件。 相反，它会选择默认组件 (进程、线程、磁盘和网络) 。 若要选择跟踪组件，请使用为 NT 内核记录器跟踪会话自定义的 TraceView 接口。

TMF 文件用于 Windows 内核跟踪 TMF，它包含在 WDK 中。 单击 " **选择 TMF 文件**"，单击 " **添加**"，导航到 " \\ 工具" \\ 跟踪 \\ i386 子目录，然后选择 "TMF"。

有关详细信息，请参阅 [创建 NT 内核记录器跟踪会话](creating-an-nt-kernel-logger-trace-session.md)。

 

 






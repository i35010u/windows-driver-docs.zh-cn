---
title: 在工作组计算机上进行远程调试
description: 您可以使用加入到工作组的计算机执行远程调试。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 995f394ce1e1114faa4ad97b68ba576132e9a5dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786959"
---
# <a name="remote-debugging-on-workgroup-computers"></a>在工作组计算机上进行远程调试


您可以使用加入到工作组的计算机执行远程调试。 首先配置将运行调试服务器的计算机。 然后激活调试服务器。 激活调试服务器后，可以从调试客户端连接到服务器。

## <a name="span-idconfiguring_the_debugging_server_computerspanspan-idconfiguring_the_debugging_server_computerspanspan-idconfiguring_the_debugging_server_computerspanconfiguring-the-debugging-server-computer"></a><span id="Configuring_the_debugging_server_computer"></span><span id="configuring_the_debugging_server_computer"></span><span id="CONFIGURING_THE_DEBUGGING_SERVER_COMPUTER"></span>配置调试服务器计算机


-   创建一个本地管理员帐户，并使用该帐户登录。
-   为活动网络启用 "文件和打印机共享"。 例如，如果活动网络是专用网络，请为专用网络启用 "文件和打印机共享"。

    可以使用 "控制面板" 启用文件和打印机共享。 例如，下面是 Windows 8 中的步骤。

    1.  打开控制面板。
    2.  单击 " **网络和 Internet** "，然后单击 " **网络和共享中心**"。 在 " **查看活动网络**" 下，记下网络 (类型，例如 "活动" 的 "专用") 。
    3.  单击 " **更改高级共享设置**"。 对于活动网络类型，选择 " **启用网络发现** "，并 **打开 "文件和打印机共享**"。
-   按照以下步骤启动远程注册表服务。

    1.  在 "命令提示符" 窗口或 "运行" 框中，输入 " **services.msc**"。
    2.  右键单击 " **远程注册表**"，然后选择 " **启动**"。
-   按照以下步骤关闭 ForceGuest 功能。

    1.  在 "命令提示符" 窗口或 "运行" 框中，输入 **regedit**。
    2.  在注册表编辑器中，将此值设置为0。

        **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ Lsa ForceGuest**

## <a name="span-idactivating_the_debugging_serverspanspan-idactivating_the_debugging_serverspanspan-idactivating_the_debugging_serverspanactivating-the-debugging-server"></a><span id="Activating_the_debugging_server"></span><span id="activating_the_debugging_server"></span><span id="ACTIVATING_THE_DEBUGGING_SERVER"></span>激活调试服务器


您可以通过调试器或使用进程服务器或 KD 连接服务器激活调试服务器。 有关详细信息，请参阅以下主题。

-   [**激活调试服务器**](activating-a-debugging-server.md)
-   [**激活进程服务器**](activating-a-process-server.md)
-   [**激活 KD 连接服务器**](activating-a-kd-connection-server.md)

## <a name="span-idactivating_the_debugging_clientspanspan-idactivating_the_debugging_clientspanspan-idactivating_the_debugging_clientspanactivating-the-debugging-client"></a><span id="Activating_the_debugging_client"></span><span id="activating_the_debugging_client"></span><span id="ACTIVATING_THE_DEBUGGING_CLIENT"></span>激活调试客户端


激活调试客户端有多种方法。 有关详细信息，请参阅以下主题。

-   [**激活调试客户端**](activating-a-debugging-client.md)
-   [**激活智能客户端**](activating-a-smart-client.md)
-   [**激活智能客户端（内核模式）**](activating-a-smart-client--kernel-mode-.md)
-   [**搜索进程服务器**](searching-for-process-servers.md)
-   [**搜索 KD 连接服务器**](searching-for-kd-connection-servers.md)

**注意**  
如果使用命名管道将调试客户端连接到调试服务器，则必须提供有权访问运行调试服务器的计算机的帐户的用户名和密码。 使用以下选项中的一个，但不能同时使用两者。

- 使用共享服务器计算机上帐户的用户名和密码的帐户登录到调试客户端计算机。
- 在调试客户端计算机上的命令提示符窗口中，输入以下命令。

  **net use \\ \\**<em>服务器</em>**\\ ipc $/user：**<em>用户名</em>

  其中 *server* 是服务器计算机的名称， *用户名* 是有权访问服务器计算机的帐户的名称。

  出现提示时，请输入 *用户名* 的密码。

 

 

 






---
title: 在工作组计算机上进行远程调试
description: 您可以执行使用加入到工作组的计算机进行远程调试。
ms.assetid: 0E740E1A-8DEA-4086-AE9D-6B135BF278B0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 058180e21b9d294f80329ad97b9b12bf7ca83376
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353587"
---
# <a name="remote-debugging-on-workgroup-computers"></a>在工作组计算机上进行远程调试


您可以执行使用加入到工作组的计算机进行远程调试。 首先配置将运行调试服务器的计算机。 然后，激活调试服务器。 调试服务器激活后，可以从调试客户端连接到服务器。

## <a name="span-idconfiguringthedebuggingservercomputerspanspan-idconfiguringthedebuggingservercomputerspanspan-idconfiguringthedebuggingservercomputerspanconfiguring-the-debugging-server-computer"></a><span id="Configuring_the_debugging_server_computer"></span><span id="configuring_the_debugging_server_computer"></span><span id="CONFIGURING_THE_DEBUGGING_SERVER_COMPUTER"></span>配置调试服务器计算机


-   创建本地管理员帐户，并使用该帐户登录。
-   启用文件和打印机共享的活动网络。 例如，如果活动网络为私有，启用文件和打印机共享的专用网络。

    可以使用控制面板启用文件和打印机共享。 例如，以下是 Windows 8 中的步骤。

    1.  打开“控制面板”。
    2.  单击**网络和 Internet** ，然后**网络和共享中心**。 下**查看活动网络**，记下 （例如，专用） 处于活动状态的网络类型。
    3.  单击**更改高级共享设置**。 对于您的活动的网络类型，选择**启用网络发现**并**启用文件和打印机共享**。
-   通过执行以下步骤启动远程注册表服务。

    1.  在命令提示符窗口或运行框中，输入**services.msc**。
    2.  右键单击**远程注册表**，然后选择**启动**。
-   通过执行以下步骤关闭 ForceGuest 功能。

    1.  在命令提示符窗口或运行框中，输入**regedit**。
    2.  在注册表编辑器中，将此值设置为 0。

        **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Lsa ForceGuest**

## <a name="span-idactivatingthedebuggingserverspanspan-idactivatingthedebuggingserverspanspan-idactivatingthedebuggingserverspanactivating-the-debugging-server"></a><span id="Activating_the_debugging_server"></span><span id="activating_the_debugging_server"></span><span id="ACTIVATING_THE_DEBUGGING_SERVER"></span>激活调试服务器


可以激活在调试器也可以使用进程服务器或 KD 连接服务器的调试服务器。 有关详细信息，请参阅以下主题。

-   [**激活调试服务器**](activating-a-debugging-server.md)
-   [**激活进程服务器**](activating-a-process-server.md)
-   [**激活 KD 连接服务器**](activating-a-kd-connection-server.md)

## <a name="span-idactivatingthedebuggingclientspanspan-idactivatingthedebuggingclientspanspan-idactivatingthedebuggingclientspanactivating-the-debugging-client"></a><span id="Activating_the_debugging_client"></span><span id="activating_the_debugging_client"></span><span id="ACTIVATING_THE_DEBUGGING_CLIENT"></span>激活调试客户端


有几种方法来激活调试客户端。 有关详细信息，请参阅以下主题。

-   [**激活调试客户端**](activating-a-debugging-client.md)
-   [**激活智能客户端**](activating-a-smart-client.md)
-   [**激活智能客户端 （内核模式）**](activating-a-smart-client--kernel-mode-.md)
-   [**搜索的进程服务器**](searching-for-process-servers.md)
-   [**正在搜索 KD 连接服务器**](searching-for-kd-connection-servers.md)

**请注意**  如果使用命名的管道连接到的调试服务器的调试客户端，必须提供用户名和有权访问运行调试服务器的计算机帐户的密码。 使用一个，但不是两个以下选项。

- 登录到具有共享的用户名和密码的调试服务器计算机上的帐户的帐户的调试客户端计算机上。
- 在调试客户端计算机上，在命令提示符窗口中，输入以下命令。

  **使用 net \\ \\**  <em>Server</em>**\\ipc$ /user:**<em>用户名</em>

  其中*服务器*是服务器计算机的名称和*用户名*是有权访问服务器计算机帐户的名称。

  当系统提示输入的密码*用户名*。

 

 

 






---
ms.assetid: D92A4E42-82F0-4034-B208-66E04F6EAB26
title: 驱动程序部署、测试和调试故障排除
description: 提供为驱动程序部署预配 Visual Studio 的故障排除技巧。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92c41da624e1f1285e0a2cc60c47cec5e3f9cb60
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364212"
---
# <a name="troubleshooting-configuration-of-driver-deployment-testing-and-debugging"></a>驱动程序部署、测试和调试配置故障排除

[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1) 中介绍了如何预配目标计算机。 这里我们将提供预配过程的一些故障排除技巧。

## <a name="span-idgeneral_tipsspanspan-idgeneral_tipsspanspan-idgeneral_tipsspangeneral-tips"></a><span id="General_tips"></span><span id="general_tips"></span><span id="GENERAL_TIPS"></span>一般技巧


-   [“配置计算机”菜单命令处于非活动状态](#configure_computers_menu_command_is_inactive)
-   [预配失败](#provisioning_fails_general_tips)

## <a name="span-idprovisioning_failsspanspan-idprovisioning_failsspanspan-idprovisioning_failsspanprovisioning-fails"></a><span id="Provisioning_fails"></span><span id="provisioning_fails"></span><span id="PROVISIONING_FAILS"></span>预配失败


-   [找不到网络路径](#domain_the_network_path_was_not_found)
-   [找不到网络名称](#domain_the_network_name_cannot_be_found)
-   [无法访问远程计算机](#domain_could_not_access_remote_machine)

## <a name="span-iddebugger_won_t_connect_or_break_inspanspan-iddebugger_won_t_connect_or_break_inspanspan-iddebugger_won_t_connect_or_break_inspandebugger-wont-connect-or-break-in"></a><span id="Debugger_won_t_connect_or_break_in"></span><span id="debugger_won_t_connect_or_break_in"></span><span id="DEBUGGER_WON_T_CONNECT_OR_BREAK_IN"></span>调试程序无法连接或强行进入


-   [调试程序网络连接](#debugger_wont_connect_network)
-   [调试程序 1394 连接](#debugger_wont_connect_1394)
-   [调试程序串行连接](#debugger_wont_connect_serial)

## <a name="span-idconfigure_computers_menu_command_is_inactivespanspan-idconfigure_computers_menu_command_is_inactivespanconfigure-computers-menu-command-is-inactive"></a><span id="configure_computers_menu_command_is_inactive"></span><span id="CONFIGURE_COMPUTERS_MENU_COMMAND_IS_INACTIVE"></span>“配置计算机”菜单命令处于非活动状态


首次启动 Microsoft Visual Studio 时，“驱动程序”  菜单上的“测试”&gt;“配置计算机”  命令可能处于非活动状态（灰显）。 如果等待大约 20 秒，之后再次单击“驱动程序”  菜单，“测试”&gt;“配置计算机”  命令将可用。

## <a name="span-idprovisioning_fails_general_tipsspanspan-idprovisioning_fails_general_tipsspanprovisioning-fails-general-tips"></a><span id="provisioning_fails_general_tips"></span><span id="PROVISIONING_FAILS_GENERAL_TIPS"></span>预配失败：一般技巧


如果预配失败，请阅读“计算机配置”窗口中的一系列消息。 通常情况下，此窗口还会显示配置日志的位置。 查看日志并记下它的位置，以便以后可以参考。

日志路径可能包含隐藏的文件夹。 例如，在以下路径中，AppData 是一个隐藏的文件夹。

C:\\Users\\*currentUser*\\AppData\\Roaming\\Microsoft\\DriverTest\\Install

日志文件的名称与此类似：

Driver Test Computer Configuration 20121115130459167.log

## <a name="span-iddomain_the_network_path_was_not_foundspanspan-iddomain_the_network_path_was_not_foundspanprovisioning-fails-the-network-path-was-not-found"></a><span id="domain_the_network_path_was_not_found"></span><span id="DOMAIN_THE_NETWORK_PATH_WAS_NOT_FOUND"></span>预配失败：找不到网络路径


开始预配目标计算机时，可能会看到一条消息：“找不到网络路径”  。

在目标计算机上，请确保你已打开“网络发现”  ，并且已为相应的网络配置文件打开了“文件和打印机共享”  。 例如，如果主计算机和目标计算机加入了网络域，你必须为**域**网络配置文件打开“网络发现”和“文件和打印机共享”。 有关详细信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。

请确保你可以从主计算机对目标计算机进行 ping 操作。 在主计算机上，打开“命令提示符”窗口，然后输入 **ping** *targetComputerName*，其中 *targetComputerName* 是目标计算机的名称。

**注意**  在看到消息“找不到网络路径”  之前，你可能会看到多条消息。 这些消息中的某些消息可能会使你认为已找到网络路径，并且预配的第一步已经成功。 事实上，网络路径并未找到，也没有任何预配部分成功。 例如，你可能会看到：

 

```cpp
Connecting to computer "MyComputer"
Installing driver test automation service
Getting computer system information
Copying driver test automation files
The network path was not found.
```

## <a name="span-iddomain_the_network_name_cannot_be_foundspanspan-iddomain_the_network_name_cannot_be_foundspanprovisioning-fails-the-network-name-cannot-be-found"></a><span id="domain_the_network_name_cannot_be_found"></span><span id="DOMAIN_THE_NETWORK_NAME_CANNOT_BE_FOUND"></span>预配失败：找不到网络名称


开始预配目标计算机时，你可能会看到一条消息：“找不到网络名称”  。 仔细检查目标计算机的名称。 如果最初输入的计算机名称不正确，请重新启动预配向导（“驱动程序”&gt;“测试”&gt;“配置计算机”）  。 选择不正确的计算机名称，然后单击“下一步”  。 在**计算机名称**中，输入正确的目标计算机名称，并完成向导。

**注意**  在看到消息“找不到网络名称”  之前，你可能会看到多条消息。 这些消息中的某些消息可能会使你认为已找到计算机名称，并且预配的第一步已经成功。 事实上，计算机名称并未找到，也没有任何预配部分成功。 例如，你可能会看到：

 

```cpp
Connecting to computer "NonExistentComputer"
Installing driver test automation service
Getting computer system information
Copying driver test automation files
The network name cannot be found.
```

**注意**  输入不正确的目标计算机名称时显示的消息可能会不同。 例如，你可能会看到一条关于启用网络发现的消息。

 

```cpp
Connecting to computer "NonExistentComputer"
Installing driver test automation service
Could not access remote machine "NonExistentComputer" over the network. 
Error:53. Automatic configuration of machines over the network requires
that network discovery and file and print sharing be enabled on the 
target machine.
```

或者系统可能会提示你输入凭据。

```cpp
Enter your password to connect to: NonExistentComputer
```

## <a name="span-iddomain_could_not_access_remote_machinespanspan-iddomain_could_not_access_remote_machinespanprovisioning-fails-could-not-access-remote-machine"></a><span id="domain_could_not_access_remote_machine"></span><span id="DOMAIN_COULD_NOT_ACCESS_REMOTE_MACHINE"></span>预配失败：无法访问远程计算机


开始预配目标计算机时，你可能会看到一条消息：“无法访问网络中的远程计算机‘computerName’”    。 此消息可能由于多种原因显示。 请确认你的主计算机和目标计算机均加入同一个域或同一工作组。 有关详细信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。 请确认你输入了正确的目标计算机名称。 请确认已在目标计算机上启用了“网络发现”和“文件和打印共享”。

## <a name="debugger-breakpoints-are-not-triggered-for-kernel-mode-driver"></a>未为内核模式驱动程序触发调试程序断点


1. 部署断点已禁用的驱动程序。 
2. 手动强行进入内核模式调试程序。 
3. 设置模块加载时的异常：
   ```cpp
   sxe ld <DriverName>
   ``` 
4. 启用断点并继续执行。 
5. 在目标计算机上，禁用设备节点，然后重新启用。 

## <a name="span-iddebugger_wont_connect_networkspanspan-iddebugger_wont_connect_networkspandebugger-wont-connect-or-break-in-network-connection"></a><span id="debugger_wont_connect_network"></span><span id="DEBUGGER_WONT_CONNECT_NETWORK"></span>调试程序无法连接或强行进入：网络连接


请确认正在调试的应用程序被允许通过所有网络类型的防火墙。

请咨询网络管理员了解允许网络调试的端口。

如果目标计算机有多个网络适配器，你必须指定要用于调试的网络适配器的总线参数。

有关详细信息，请参阅[通过网络电缆进行调试的故障排除技巧](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)

## <a name="span-iddebugger_wont_connect_1394spanspan-iddebugger_wont_connect_1394spandebugger-wont-connect-or-break-in-1394-connection"></a><span id="debugger_wont_connect_1394"></span><span id="DEBUGGER_WONT_CONNECT_1394"></span>调试程序无法连接或强行进入：1394 连接


如果目标计算机有多个 1394 控制器，你必须指定要用于调试的 1394 控制器的总线参数。 有关详细信息，请参阅[通过 1394 电缆进行调试的故障排除技巧](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-1394-cable-connection)。

## <a name="span-iddebugger_wont_connect_serialspanspan-iddebugger_wont_connect_serialspandebugger-wont-connect-or-break-in--serial-connection"></a><span id="debugger_wont_connect_serial"></span><span id="DEBUGGER_WONT_CONNECT_SERIAL"></span>调试程序无法连接或强行进入：串行连接


检查主计算机和目标计算机上的 COM 端口号。 请确认你为主计算机和目标计算机上的调试配置了相同的波特率。 有关详细信息，请参阅[通过串行电缆进行调试的故障排除技巧](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-null-modem-cable-connection-in-visual-studio)

 

 






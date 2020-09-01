---
title: 在 Visual Studio 中设置虚拟机的内核模式调试
description: 你可以使用 Microsoft Visual Studio 来设置和执行虚拟机的内核模式调试。
ms.assetid: E7A289CA-29CE-4C6F-AD08-529E58379715
ms.date: 10/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3607ba23837c3456d941a89061d941fdf632d5c2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216006"
---
# <a name="setting-up-kernel-mode-debugging-of-a-virtual-machine-in-visual-studio"></a>在 Visual Studio 中设置虚拟机的内核模式调试

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

你可以使用 Microsoft Visual Studio 来设置和执行虚拟机的内核模式调试。 虚拟机可以与调试器位于同一台物理计算机上，也可以位于连接到同一网络的其他计算机上。 若要将 Visual Studio 用于内核模式调试，你必须将 Windows 驱动程序工具包 (WDK) 与 Visual Studio 集成。 有关如何安装集成环境的信息，请参阅 [使用 Visual Studio 进行调试](debugging-using-visual-studio.md)。

运行调试器的计算机称为 " *主机*"，正在调试的虚拟机称为 " *目标虚拟机*"。

## <a name="span-idconfiguring_the_target_virtual_machinespanspan-idconfiguring_the_target_virtual_machinespanspan-idconfiguring_the_target_virtual_machinespanconfiguring-the-target-virtual-machine"></a><span id="Configuring_the_Target_Virtual_Machine"></span><span id="configuring_the_target_virtual_machine"></span><span id="CONFIGURING_THE_TARGET_VIRTUAL_MACHINE"></span>正在配置目标虚拟机


1. 在虚拟机中，在提升的命令提示符窗口中输入以下命令。

   **bcdedit/debug on**

   **bcdedit/dbgsettings 串行 debugport：**<em>n</em> **波特率： 115200**

   其中， *n* 是虚拟机上的 COM 端口的编号。

2. 重新启动虚拟机。
3. 在虚拟机中，将 COM 端口配置为映射到命名管道。 调试器将通过此管道进行连接。 有关如何创建此管道的详细信息，请参阅虚拟机的文档。

## <a name="span-idconfiguring_the_host_computerspanspan-idconfiguring_the_host_computerspanspan-idconfiguring_the_host_computerspanconfiguring-the-host-computer"></a><span id="Configuring_the_Host_Computer"></span><span id="configuring_the_host_computer"></span><span id="CONFIGURING_THE_HOST_COMPUTER"></span>配置主机计算机


主计算机可以是运行虚拟机的同一物理计算机，也可以是单独的计算机。

1. 在主计算机上的 Visual Studio 中，在 " **驱动程序** " 菜单上选择 "测试" " ** &gt; 配置计算机**"。
2. 单击 " **添加新计算机**"。
3. 对于 " **计算机名称**"，请输入运行目标虚拟机的物理计算机的名称。
4. 选择 " **手动配置调试器并不设置**"，然后单击 " **下一步**"。
5. 对于 " **连接类型**"，请选择 " **串行**"。
6. 选中 " **管道**"，然后选中 " **重新连接**"。
7. 如果调试器在虚拟机所在的同一台计算机上运行，请输入以下 **管道名称**：

   **\\\\.\\管道 \\ **<em>PipeName</em>。

   如果调试器在不同于虚拟机的计算机上运行，请在 " **管道名称**" 中输入以下内容：

   **\\\\**<em>VMHost</em>** \\ 管道 \\ **<em>PipeName</em>

   其中， *VMHost* 是运行目标虚拟机的物理计算机的名称， *PipeName* 是与目标虚拟机上的 COM 端口关联的管道的名称。

8. 单击“下一步”  。 单击“完成”。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  在主计算机上，在 Visual Studio 的 " **调试** " 菜单中，选择 " **附加到进程**"。
2.  对于 " **传输**"，请选择 " **Windows 内核模式调试程序**"。
3.  对于 " **限定符**"，请选择运行目标虚拟机的物理计算机的名称。
4.  单击 **“附加”** 。

>[!TIP] 
> 如果收到 "无法启动调试会话，错误8007005：访问被拒绝" 消息，请在主计算机上以管理员身份运行 Visual Studio。 

## <a name="span-idgeneration_2_virtual_machinesspanspan-idgeneration_2_virtual_machinesspangeneration-2-virtual-machines"></a><span id="generation_2_virtual_machines"></span><span id="GENERATION_2_VIRTUAL_MACHINES"></span>第2代虚拟机


默认情况下，第2代虚拟机中不显示 COM 端口。 可以通过 PowerShell 或 WMI 添加 COM 端口。 要使 COM 端口显示在 Hyper-v 管理器控制台中，必须使用路径创建这些端口。

若要使用第2代虚拟机上的 COM 端口启用内核调试，请按照以下步骤操作：

1. 通过输入以下 PowerShell 命令来禁用安全启动：

   **Set-vmfirmware – Vmname** *Vmname* **– EnableSecureBoot Off**

   其中， *VmName* 是虚拟机的名称。

2. 输入以下 PowerShell 命令，将 COM 端口添加到虚拟机：

   **Set-vmcomport – VMName** *VMName* **1 \\ \\ 。 \\管道 \\ **<em>PipeName</em>

   例如，以下命令将虚拟机 TestVM 上的第一个 COM 端口配置为连接到本地计算机上的命名管道 TestPipe。

   **Set-vmcomport – VMName TestVM 1 \\ \\ 。 \\管道 \\ TestPipe**

3. 重新启动 VM，使新设置生效。

有关详细信息，请参阅[第 2 代虚拟机概述](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282285(v=ws.11))。


## <a name="span-idfirewallsspantroubleshooting-firewalls-and-network-access-issues"></a><span id="Firewalls"></span>防火墙和网络访问问题疑难解答

你的调试器 (WinDbg 或 KD) 必须具有通过防火墙的访问权限。 这甚至是网络适配器支持的虚拟串行端口的情况。

如果在加载调试器时 Windows 提示你关闭防火墙，请选择 **所有三个** 框。

根据所使用的 VM 的具体情况，可能需要更改虚拟机的网络设置，以将其桥接到 Microsoft 内核网络调试适配器。 否则，虚拟机将无法访问网络。

**Windows 防火墙**

可以使用 "控制面板" 允许通过 Windows 防火墙进行访问。 

1. 打开 "控制面板 > 系统和安全"，然后选择 "允许应用通过 Windows 防火墙"。 
2. 在应用程序列表中，找到 " *WINDOWS GUI 符号调试器* " 和 " *windows 内核调试器*"。 
3. 使用此复选框可以通过防火墙允许这两个应用程序。 单击“确定”保存设置。
4.  (WinDbg 或 KD) 重新启动调试应用程序。


## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设置虚拟机主机的网络调试](setting-up-network-debugging-of-a-virtual-machine-host.md)
 


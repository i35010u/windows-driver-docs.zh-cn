---
title: 在 Visual Studio 中设置虚拟机的内核模式调试
description: 可以使用 Microsoft Visual Studio 设置和执行虚拟机的内核模式调试。
ms.assetid: E7A289CA-29CE-4C6F-AD08-529E58379715
ms.date: 10/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: fa784a5cdb58fdcdb0830978688503f6b6e6e01f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381935"
---
# <a name="setting-up-kernel-mode-debugging-of-a-virtual-machine-in-visual-studio"></a>在 Visual Studio 中设置虚拟机的内核模式调试

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

可以使用 Microsoft Visual Studio 设置和执行虚拟机的内核模式调试。 虚拟机可以位于与调试器相同的物理计算机上，也可以连接到同一网络的不同计算机上。 若要使用内核模式调试的 Visual Studio，必须具有 Windows Driver Kit (WDK) 与 Visual Studio 集成。 有关如何安装集成的环境的信息，请参阅[Windows 驱动程序开发](https://go.microsoft.com/fwlink/p?linkid=301383)。

运行调试器的计算机称为*主机计算机*，并调用正在调试的虚拟机*目标虚拟机*。

## <a name="span-idconfiguringthetargetvirtualmachinespanspan-idconfiguringthetargetvirtualmachinespanspan-idconfiguringthetargetvirtualmachinespanconfiguring-the-target-virtual-machine"></a><span id="Configuring_the_Target_Virtual_Machine"></span><span id="configuring_the_target_virtual_machine"></span><span id="CONFIGURING_THE_TARGET_VIRTUAL_MACHINE"></span>配置目标虚拟机


1. 在虚拟机，在提升的命令提示符窗口，输入以下命令。

   **bcdedit /debug 上**

   **bcdedit /dbgsettings 串行 debugport:**<em>n</em> **baudrate:115200**

   其中*n*是虚拟机上的 COM 端口的数目。

2. 重新启动虚拟机。
3. 虚拟机中配置的 COM 端口映射到命名管道。 调试器将通过此管道连接。 有关如何创建此管道的详细信息，请参阅虚拟机的文档。

## <a name="span-idconfiguringthehostcomputerspanspan-idconfiguringthehostcomputerspanspan-idconfiguringthehostcomputerspanconfiguring-the-host-computer"></a><span id="Configuring_the_Host_Computer"></span><span id="configuring_the_host_computer"></span><span id="CONFIGURING_THE_HOST_COMPUTER"></span>配置主计算机


主机计算机可以是同一物理计算机运行虚拟机，也可以是单独的计算机。

1. 上，在 Visual Studio 中，主机计算机上**驱动程序**菜单中，选择**测试&gt;配置计算机**。
2. 单击**添加新的计算机**。
3. 有关**计算机名**，输入正在运行目标虚拟机的物理计算机的名称。
4. 选择**手动配置调试器并不设置**，然后单击**下一步**。
5. 有关**连接类型**，选择**串行**。
6. 检查**管道**，并检查**重新连接**。
7. 如果调试器运行在虚拟机所在的计算机上，输入以下项作为**管道名称**:

   **\\\\.\\管道\\**<em>PipeName</em>。

   如果调试器正在从虚拟机的不同计算机上，输入以下项作为**管道名称**:

   **\\\\**<em>VMHost</em>**\\pipe\\**<em>PipeName</em>

   其中， *VMHost*运行目标虚拟机，请在物理计算机的名称和*PipeName*是与目标虚拟机上的 COM 端口关联的管道的名称。

8. 单击“下一步” 。 单击 **“完成”**。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  上，在 Visual Studio 中，主机计算机上**调试**菜单中，选择**附加到进程**。
2.  有关**传输**，选择**Windows 内核模式调试程序**。
3.  有关**限定符**，选择正在运行目标虚拟机的物理计算机的名称。
4.  单击**附加**。

>[!TIP] 
> 如果你将收到消息"无法启动调试会话，错误 8007005:拒绝访问"，在主计算机上以管理员身份运行 Visual Studio。 

## <a name="span-idgeneration2virtualmachinesspanspan-idgeneration2virtualmachinesspangeneration-2-virtual-machines"></a><span id="generation_2_virtual_machines"></span><span id="GENERATION_2_VIRTUAL_MACHINES"></span>第 2 代虚拟机


默认情况下，COM 端口不显示在第 2 代虚拟机中。 可以添加通过 PowerShell 或 WMI 的 COM 端口。 要在 Hyper-v 管理器控制台中显示的 COM 端口，则必须创建使用路径。

若要启用内核调试第 2 代虚拟机上使用 COM 端口，请执行以下步骤：

1. 通过输入以下 PowerShell 命令来禁用安全启动：

   **Set-VMFirmware –Vmname** *VmName* **–EnableSecureBoot Off**

   其中*VmName*是你的虚拟机的名称。

2. 将 COM 端口添加到虚拟机中，通过输入此 PowerShell 命令：

   **Set-VMComPort –VMName** *VmName* **1 \\\\.\\pipe\\**<em>PipeName</em>

   例如，以下命令在虚拟机 TestVM 以连接到命名管道 TestPipe 本地计算机上的配置的第一个 COM 端口。

   **Set-vmcomport – VMName TestVM 1 \\ \\。\\管道\\TestPipe**

3. 重新启动 VM，使新设置是在起作用。

有关详细信息，请参阅[第 2 代虚拟机概述](https://go.microsoft.com/fwlink/p/?Linkid=331326)。


## <a name="span-idfirewallsspantroubleshooting-firewalls-and-network-access-issues"></a><span id="Firewalls"></span>防火墙和网络访问问题疑难解答

调试器 （WinDbg 或 KD） 必须具有通过防火墙进行访问。 这甚至可以是虚拟串行端口支持的网络适配器，这种情况。

如果 Windows 提示你关闭防火墙，调试程序时加载，请选择**所有这三个**框。

具体取决于在使用 VM 的详细信息，可能需要更改要到 Microsoft 内核调试的网卡桥接各虚拟机的网络设置。 否则，虚拟机将不具有网络访问权限。

**Windows 防火墙**

可以使用控制面板以允许通过 Windows 防火墙的访问。 

1. 打开控制面板 > 系统和安全性，并选择允许通过 Windows 防火墙的应用程序。 
2. 在应用程序列表中，找到*Windows GUI 符号调试器*并*Windows 内核调试程序*。 
3. 使用复选框以允许通过防火墙这些两个应用程序。 单击“确定”保存设置。
4. 重新启动调试应用程序 （WinDbg 或 KD）。


## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设置网络调试的虚拟机主机](setting-up-network-debugging-of-a-virtual-machine-host.md)
 

 







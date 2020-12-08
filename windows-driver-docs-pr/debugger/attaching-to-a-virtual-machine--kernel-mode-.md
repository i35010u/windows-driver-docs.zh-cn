---
title: 使用虚拟 COM 端口手动设置虚拟机 Kernel-Mode 调试
description: 适用于 Windows 的调试工具支持使用虚拟 COM 端口对虚拟机进行内核调试。
keywords:
- 虚拟机调试
- 虚拟 PC 调试
- VMware 调试
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 33fee84ec192c71885d62fd0b7aa8fb361a2ea9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819291"
---
# <a name="setting-up-kernel-mode-debugging-of-a-virtual-machine-manually-using-a-virtual-com-port"></a>使用虚拟 COM 端口手动设置虚拟机 Kernel-Mode 调试

适用于 Windows 的调试工具支持虚拟机的内核调试。 虚拟机可以与调试器位于同一台物理计算机上，也可以位于连接到同一网络的其他计算机上。 本主题介绍如何通过 KDCOM 使用虚拟 COM 端口手动设置虚拟机的调试。

使用 KDNET 虚拟网络是一种更快的选择，建议使用。 有关详细信息，请参阅 [使用 KDNET 设置虚拟机的网络调试](setting-up-network-debugging-of-a-virtual-machine-host.md)。


## <a name="span-idsetting_up_the_target_virtual_machinespanspan-idsetting_up_the_target_virtual_machinespanspan-idsetting_up_the_target_virtual_machinespansetting-up-the-target-virtual-machine"></a><span id="Setting_Up_the_Target_Virtual_Machine"></span><span id="setting_up_the_target_virtual_machine"></span><span id="SETTING_UP_THE_TARGET_VIRTUAL_MACHINE"></span>设置目标虚拟机

运行调试器的计算机称为 *主机计算机*，被调试的虚拟机称为 *目标虚拟机*。

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

1. 在虚拟机中，在提升的命令提示符窗口中输入以下命令。

   **bcdedit/debug on**

   **bcdedit/dbgsettings 串行 debugport：**<em>n</em> **波特率： 115200**

   其中， *n* 是虚拟机上的 COM 端口的编号。 

2. 在虚拟机中，将 COM 端口配置为映射到命名管道。 调试器将通过此管道进行连接。 有关如何创建此管道的详细信息，请参阅虚拟机的文档。

3. 在提升模式下启动调试器，例如在管理员命令提示符下启动。 在通过串行管道调试 VM 时，必须在提升模式下运行调试器。  调试器附加并运行后，请重新启动目标 VM。


## <a name="span-idstarting_the_debuggerspanspan-idstarting_the_debuggerspanstarting-the-debugging-session-using-windbg"></a><span id="starting_the_debugger"></span><span id="STARTING_THE_DEBUGGER"></span>使用 WinDbg 启动调试会话

在主计算机上，以管理员身份打开 WinDbg。 在通过串行管道调试 VM 时，必须在提升模式下运行调试器。 在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **COM** " 选项卡。选中 " **管道** " 框，并选中 " **重新连接** " 框。 对于 **波特率**，请输入115200。 对于 " **重置**"，请输入0。

如果调试器在虚拟机所在的同一台计算机上运行，请输入以下端口作为 **端口**。

**\\\\.\\管道 \\**<em>PipeName</em>。

如果调试器在不同于虚拟机的计算机上运行，请输入以下 **端口作为端口**。

**\\\\**<em>VMHost</em>**\\ 管道 \\**<em>PipeName</em>

选择“确定”。

还可以在命令行中启动 WinDbg。 如果调试器在虚拟机所在的物理计算机上运行，请在命令提示符窗口中输入以下命令。

**windbg-k com：管道，端口 = \\ \\ 。 \\管道 \\**<em>PipeName</em>**，重置 = 0，重新连接**

如果调试器在不同于虚拟机的物理计算机上运行，请在命令提示符窗口中输入以下命令。

**windbg-k com：管道，端口 = \\ \\**<em>VMHost</em>**\\ 管道 \\**<em>PipeName</em>**，重置 = 0，重新连接**

## <a name="span-idstarting_the_debugging_session_using_kdspanspan-idstarting_the_debugging_session_using_kdspanspan-idstarting_the_debugging_session_using_kdspanstarting-the-debugging-session-using-kd"></a><span id="Starting_the_Debugging_Session_Using_KD"></span><span id="starting_the_debugging_session_using_kd"></span><span id="STARTING_THE_DEBUGGING_SESSION_USING_KD"></span>使用 KD 启动调试会话


若要调试与调试器运行在同一物理计算机上的虚拟机，请在 *提升* 的命令提示符窗口中输入以下命令。

**kd-k com： pipe、port = \\ \\ 。 \\管道 \\**<em>PipeName</em>**，重置 = 0，重新连接**

若要从调试器调试在不同物理计算机上运行的虚拟机，请在命令提示符窗口中输入以下命令。

**kd-k com：管道，端口 = \\ \\**<em>VMHost</em>**\\ 管道 \\**<em>PipeName</em>**，重置 = 0，重新连接**

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________VMHost"></span><span id="________vmhost"></span><span id="________VMHOST"></span>*VMHost*  
指定正在运行虚拟机的计算机的名称。

<span id="PipeName_______"></span><span id="pipename_______"></span><span id="PIPENAME_______"></span>*PipeName*   
指定在虚拟机上创建的管道的名称。

<span id="resets_0"></span><span id="RESETS_0"></span>**重置 = 0**  
指定当主机和目标正在同步时，可以将不限数量的重置数据包发送到目标。 对 Microsoft Virtual PC 和管道丢弃多余字节的其他虚拟机使用 **重置 = 0** 参数。 不要将此参数用于 VMware 或其他不删除多余字节的虚拟机。

<span id="________reconnect"></span><span id="________RECONNECT"></span>*重新连接*  
如果发生读/写失败，则使调试器自动断开连接并重新连接管道。 此外，如果调试器在启动调试器时找不到命名管道，则 *reconnect* 参数会使调试器等待名为 *PipeName* 的管道出现。 在计算机重新启动期间，对虚拟 PC 和其他销毁并重新创建管道的虚拟机使用 *重新连接* 。 不要将此参数用于 VMware 或其他虚拟机，这些虚拟机在计算机重新启动时保留其管道。

有关其他命令行选项的详细信息，请参阅 [**KD Command-Line options**](kd-command-line-options.md) 或 [**WinDbg Command-Line options**](windbg-command-line-options.md)。

## <a name="span-idgeneration_2_virtual_machinesspanspan-idgeneration_2_virtual_machinesspangeneration-2-virtual-machines"></a><span id="generation_2_virtual_machines"></span><span id="GENERATION_2_VIRTUAL_MACHINES"></span>第2代虚拟机


默认情况下，第2代虚拟机中不显示 COM 端口。 可以通过 PowerShell 或 WMI 添加 COM 端口。 要使 COM 端口显示在 Hyper-v 管理器控制台中，必须使用路径创建这些端口。

若要使用第2代虚拟机上的 COM 端口启用内核调试，请按照以下步骤操作：

1. 通过输入以下 PowerShell 命令来禁用安全启动：

   **Set-vmfirmware – Vmname** *Vmname* **– EnableSecureBoot Off**

   其中， *VmName* 是虚拟机的名称。

2. 输入以下 PowerShell 命令，将 COM 端口添加到虚拟机：

   **Set-vmcomport – VMName** *VMName* **1 \\ \\ 。 \\管道 \\**<em>PipeName</em>

   例如，以下命令将虚拟机 TestVM 上的第一个 COM 端口配置为连接到本地计算机上的命名管道 TestPipe。

   **Set-vmcomport – VMName TestVM 1 \\ \\ 。 \\管道 \\ TestPipe**


3. 调试器附加并运行后，停止并冷启动 VM，以激活 VM 中的 COM 端口。模拟的 UARTS 不可用于调试，除非使用管道名称实际配置了至少一个管道，并且无法对其进行热添加。

4. 完成配置更改更新后，重新启用安全启动。

有关第2代 Vm 的详细信息，请参阅 [第2代虚拟机概述](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282285(v=ws.11))。


## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


如果目标计算机已停止响应，则目标计算机仍会因为较早的内核调试操作而停止，或者使用了 **-b** [命令行选项](command-line-options.md)，调试器会立即进入目标计算机。

否则，目标计算机将继续运行，直到调试器使其中断。


## <a name="span-idfirewallsspantroubleshooting-firewalls-and-network-access-issues"></a><span id="Firewalls"></span>防火墙和网络访问问题疑难解答

你的调试器 (WinDbg 或 KD) 必须具有通过防火墙的访问权限。 这甚至是网络适配器支持的虚拟串行端口的情况。

如果在加载调试器时 Windows 提示你关闭防火墙，请选择所有三个框。

根据所使用的 VM 的具体情况，可能需要更改虚拟机的网络设置，以将其桥接到 Microsoft 内核网络调试适配器。 否则，虚拟机将无法访问网络。

**Windows 防火墙**

可以使用 "控制面板" 允许通过 Windows 防火墙进行访问。 打开 "控制面板 > 系统和安全"，然后选择 "允许应用通过 Windows 防火墙"。 在应用程序列表中，找到 " *WINDOWS GUI 符号调试器* " 和 " *windows 内核调试器*"。 使用此复选框可以通过防火墙允许这两个应用程序。  (WinDbg 或 KD) 重新启动调试应用程序。


## <a name="span-idthird_party_vmsspanthird-party-vms"></a><span id="Third_Party_VMs"></span>第三方 Vm

**VMWare**  
如果使用 VMWare 设施重启虚拟机 (例如，"重置" 按钮) "，请退出 WinDbg，然后重新启动 WinDbg 以继续调试。 在虚拟机调试期间，VMWare 通常会消耗100% 的 CPU。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[使用 KDNET 设置虚拟机的网络调试](setting-up-network-debugging-of-a-virtual-machine-host.md)

[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

[设置虚拟机主机的网络调试](setting-up-network-debugging-of-a-virtual-machine-host.md)

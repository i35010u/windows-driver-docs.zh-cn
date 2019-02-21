---
title: 设置内核模式调试的虚拟机手动使用虚拟 COM 端口
description: 调试工具的 Windows 支持内核调试的虚拟机使用虚拟 COM 端口。
ms.assetid: e863e664-8338-4bbe-953b-e000a6843db9
keywords:
- 虚拟机调试
- 虚拟 PC 调试
- VMware 调试
ms.date: 05/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: f29242c1042805498cca354902c415ff8485796f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523112"
---
# <a name="setting-up-kernel-mode-debugging-of-a-virtual-machine-manually-using-a-virtual-com-port"></a>设置内核模式调试的虚拟机手动使用虚拟 COM 端口

调试工具的 Windows 支持内核调试的虚拟机。 虚拟机可以位于与调试器相同的物理计算机上，也可以连接到同一网络的不同计算机上。 本主题介绍如何设置虚拟机使用虚拟 COM 端口 KDCOM 通过手动的调试。

使用 KDNET 虚拟网络是更快的做法，建议。 有关详细信息，请参阅[设置网络调试的虚拟机与 KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)。


## <a name="span-idsettingupthetargetvirtualmachinespanspan-idsettingupthetargetvirtualmachinespanspan-idsettingupthetargetvirtualmachinespansetting-up-the-target-virtual-machine"></a><span id="Setting_Up_the_Target_Virtual_Machine"></span><span id="setting_up_the_target_virtual_machine"></span><span id="SETTING_UP_THE_TARGET_VIRTUAL_MACHINE"></span>设置目标虚拟机

运行调试器的计算机称为*主机计算机*，并调用正在调试的虚拟机*目标虚拟机*。

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。

1. 在虚拟机，在提升的命令提示符窗口，输入以下命令。

   **bcdedit /debug 上**

   **bcdedit /dbgsettings 串行 debugport:**<em>n</em> **baudrate:115200**

   其中*n*是虚拟机上的 COM 端口的数目。

2. 虚拟机中配置的 COM 端口映射到命名管道。 调试器将通过此管道连接。 有关如何创建此管道的详细信息，请参阅虚拟机的文档。

3. 附加并运行调试器后，重新启动目标计算机。


## <a name="span-idstartingthedebuggerspanspan-idstartingthedebuggerspanstarting-the-debugging-session-using-windbg"></a><span id="starting_the_debugger"></span><span id="STARTING_THE_DEBUGGER"></span>开始使用 WinDbg 调试会话

在主计算机上打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**COM**选项卡。检查**管道**框中，并检查**重新连接**框。 有关**波特率**，输入 115200。 有关**重置**，输入 0。

如果调试器运行在虚拟机所在的计算机上，输入以下项作为**端口**。

**\\\\.\\管道\\**<em>PipeName</em>。

如果调试器正在从虚拟机的不同计算机上，输入以下项作为**端口**。

**\\\\**<em>VMHost</em>**\\pipe\\**<em>PipeName</em>

单击“确定” 。

此外可以在命令行启动 WinDbg。 如果在同一台物理计算机作为虚拟机上运行调试器，请在命令提示符窗口中输入以下命令。

**windbg -k com:pipe,port=\\\\.\\pipe\\**<em>PipeName</em>**,resets=0,reconnect**

如果从虚拟机的不同物理计算机上运行调试器，请在命令提示符窗口中输入以下命令。

**windbg -k com:pipe,port=\\\\**<em>VMHost</em>**\\pipe\\**<em>PipeName</em>**,resets=0,reconnect**

## <a name="span-idstartingthedebuggingsessionusingkdspanspan-idstartingthedebuggingsessionusingkdspanspan-idstartingthedebuggingsessionusingkdspanstarting-the-debugging-session-using-kd"></a><span id="Starting_the_Debugging_Session_Using_KD"></span><span id="starting_the_debugging_session_using_kd"></span><span id="STARTING_THE_DEBUGGING_SESSION_USING_KD"></span>启动调试会话使用 KD


若要调试在调试器所在的物理计算机运行的虚拟机，请在命令提示符窗口中输入以下命令。

**kd-k com:pipe，端口 =\\\\。\\管道\\**<em>PipeName</em>**，重置 = 0 时，重新连接**

若要调试在调试器中的不同物理计算机运行的虚拟机，请在命令提示符窗口中输入以下命令。

**kd -k com:pipe,port=\\\\**<em>VMHost</em>**\\pipe\\**<em>PipeName</em>**,resets=0,reconnect**

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________VMHost"></span><span id="________vmhost"></span><span id="________VMHOST"></span> *VMHost*  
指定虚拟机运行的计算机的名称。

<span id="PipeName_______"></span><span id="pipename_______"></span><span id="PIPENAME_______"></span>*PipeName*   
指定在虚拟机创建的管道的名称。

<span id="resets_0"></span><span id="RESETS_0"></span>**resets=0**  
指定无限的数量的重置数据包可以发送到目标中，同步主机和目标时。 使用**重置 = 0** Microsoft Virtual PC 和其管道删除多余的字节数的其他虚拟机的参数。 VMware 或其管道不会删除所有多余的字节数的其他虚拟机不使用此参数。

<span id="________reconnect"></span><span id="________RECONNECT"></span> *reconnect*  
使调试器自动断开连接并在读/写失败时重新连接管道。 此外，如果调试器启动调试器时，不到命名的管道*重新连接*参数会导致调试程序等待名为管道*PipeName*才会显示。 使用*重新连接*Virtual PC 和销毁并重新创建其管道，在一台计算机的其他虚拟机重新启动。 VMware 或其他虚拟机时，在计算机重启过程中保留其管道不使用此参数。

有关其他命令行选项的详细信息，请参阅[ **KD 命令行选项**](kd-command-line-options.md)或[ **WinDbg 命令行选项**](windbg-command-line-options.md).

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


3. 附加并运行调试器后，停止和冷启动 VM 后，若要激活的 COM 端口在 VM 中。　模拟的 UARTS 不适用于调试除非至少一个实际配置为管道名称，但是它们不能为热添加。

4. 重新启用安全启动，完成后更新的配置更改。

有关第 2 代 Vm 的详细信息，请参阅[第 2 代虚拟机概述](https://go.microsoft.com/fwlink/p/?Linkid=331326)。


## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


如果目标计算机已停止响应，由于早期的内核调试操作，而仍停止目标计算机，或者您使用 **-b** [命令行选项](command-line-options.md)，调试器将中断立即目标计算机。

否则，目标计算机将继续运行，直到调试程序进行排序它执行中断。


## <a name="span-idfirewallsspantroubleshooting-firewalls-and-network-access-issues"></a><span id="Firewalls"></span>防火墙和网络访问问题疑难解答

调试器 （WinDbg 或 KD） 必须具有通过防火墙进行访问。 这甚至可以是虚拟串行端口支持的网络适配器，这种情况。

如果 Windows 提示你关闭防火墙，加载调试器时，选择所有三个框。

具体取决于在使用 VM 的详细信息，可能需要更改要到 Microsoft 内核调试的网卡桥接各虚拟机的网络设置。 否则，虚拟机将不具有网络访问权限。

**Windows 防火墙**

可以使用控制面板以允许通过 Windows 防火墙的访问。 打开控制面板 > 系统和安全性，并选择允许通过 Windows 防火墙的应用程序。 在应用程序列表中，找到*Windows GUI 符号调试器*并*Windows 内核调试程序*。 使用复选框以允许通过防火墙这些两个应用程序。 重新启动调试应用程序 （WinDbg 或 KD）。


## <a name="span-idthirdpartyvmsspanthird-party-vms"></a><span id="Third_Party_VMs"></span>第三方虚拟机

**VMWare**   如果使用 VMWare 工具 （例如，重置按钮） 重新启动虚拟机，退出的 WinDbg 中，，然后重新启动 WinDbg，若要继续调试。 虚拟机在调试期间，VMWare 通常会占用 100%的 CPU。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题

[设置网络调试 KDNET 具有的虚拟机](setting-up-network-debugging-of-a-virtual-machine-host.md)

[内核模式调试手动设置](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

[设置网络调试的虚拟机主机](setting-up-network-debugging-of-a-virtual-machine-host.md)
 







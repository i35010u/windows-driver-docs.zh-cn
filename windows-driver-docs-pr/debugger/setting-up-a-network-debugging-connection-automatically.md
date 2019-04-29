---
title: 自动设置 KDNET 网络内核调试
description: 使用 KDNET 配置网络内核调试会自动为 Windows 调试工具。
ms.assetid: B4A79B2E-D4B1-42CA-9121-DEC923C76927
keywords:
- 网络调试
- 以太网调试
- WinDbg
- KDNET
ms.date: 09/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: d33e84652f94172fa4df340ae488450cee94615f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381948"
---
# <a name="setting-up-kdnet-network-kernel-debugging-automatically"></a>自动设置 KDNET 网络内核调试

调试工具的 Windows 支持通过网络内核调试。 本主题介绍如何设置网络会自动使用 kdnet.exe 安装工具进行调试。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。 在主计算机必须运行 Windows 7 或更高版本，并在目标计算机必须运行 Windows 8 或更高版本。



## <a name="span-iddeterminingtheipaddressofthehostcomputerspanspan-iddeterminingtheipaddressofthehostcomputerspanspan-iddeterminingtheipaddressofthehostcomputerspandetermining-the-ip-address-of-the-host-computer"></a><span id="Determining_the_IP_Address_of_the_Host_Computer"></span><span id="determining_the_ip_address_of_the_host_computer"></span><span id="DETERMINING_THE_IP_ADDRESS_OF_THE_HOST_COMPUTER"></span>确定主机计算机的 IP 地址

1. 确认目标和主机 Pc 连接到网络集线器或切换使用相应的网络电缆。 

2. 主计算机上打开命令提示符窗口并输入*IPConfig*若要显示的 IP 配置。 

3. 在命令输出中，找到以太网适配器的 IPv4 地址。

    ```console
    ...

    Ethernet adapter Ethernet:
    ...

    IPv4 Address. . . . . . . . . . . : <YourHostIPAddress>
    ...

    ```
4. 记下你想要用于调试的网络适配器的 IPv4 地址。

 

## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-host-and-target-computers"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>设置主机和目标计算机

使用 kdnet.exe 实用程序自动配置调试器设置目标 PC 上，通过执行以下步骤。

1. 确认主机系统上安装了 Windows 调试工具。 有关下载和安装调试器工具的信息，请参阅[的 Windows 中下载调试的工具](debugger-download-tools.md)。 

2. 找到*kdnet.exe*并*VerifiedNICList.xml*文件。 默认情况下，它们位于此处。

   ```console
   C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
   ```

   > [!NOTE]
   > 这些说明假定这两台 Pc 上的目标和主机运行 Windows 的 64 位版本。 如果这不是这样，最好的方法是运行在目标主机上运行工具的同一"位数"。 例如，如果目标正在运行 32 位 Windows，请在主机上运行 32 版本的调试器。 有关详细信息，请参阅[选择 32 位或 64 位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。
   > 

3. 在主机上将两个文件复制到网络共享或拇指驱动器，以便它们可在目标计算机上。

4. 在目标计算机上创建一个 C:\KDNET 目录并复制*kdnet.exe*并*VerifiedNICList.xml*文件复制到该目录。

   > [!IMPORTANT]
   > 使用 kdnet 若要更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
   > 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。


5. 在目标计算机上，以管理员身份打开命令提示符窗口。 输入以下命令以验证目标计算机具有支持的网络适配器。

   ```console
   C:\KDNET>kdnet
   Network debugging is supported on the following NICs:
   busparams=1.0.0, Broadcom NetXtreme Gigabit Ethernet, Plugged in.  
   This Microsoft hypervisor supports using KDNET in guest VMs.
   ```

6. 如 kdnet 输出将指示该网络适配器上支持的目标，我们可以继续操作。

7. 此命令设置主机系统的 IP 地址和生成的唯一连接密钥类型。 使用 IP 地址或主机系统的名称。 对于每个目标/主机对选取一个唯一的端口地址与在 50000 50039 的建议的范围中，工作。

   ```console
   C:\>kdnet <HostComputerIPAddress> <YourDebugPort> 
   
   Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
   Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
   ```

8. 将返回的键复制到记事本.txt 文件。


## <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspan-using-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span> 使用 WinDbg

在主计算机上打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**Net**选项卡。粘贴在你的端口号和到记事本.txt 文件中之前保存的密钥。 单击 **“确定”**。

您还可以通过打开命令提示符窗口并输入以下命令，启动 WinDbg 会话其中<YourPort>是，上面所选的端口和<YourKey>是 kdnet 上面返回的密钥。 粘贴该密钥，因为您保存到记事本.txt 文件中前面。

   ```console
  windbg -k net:port=<YourDebugPort>,key=<YourKey> 
   ```

如果系统提示有关允许 WinDbg 能够通过防火墙访问端口，允许访问的端口的 WinDbg**所有这三个**的不同网络类型。

![windows 安全警报的 windows 防火墙已阻止此应用的某些功能 ](images/debuglab-image-firewall-dialog-box.png)


## <a name="span-idrestartingtargetspanspan-idrestartingtargetspanspan-idrestartingtargetspan-restarting-the-target-pc"></a><span id="Restarting_Target"></span><span id="restarting_target"></span><span id="RESTARTING_TARGET"></span> 重新启动目标 PC

调试器连接后，重新启动目标计算机。 不要重新启动 PC，一种方法是使用此命令从管理员命令提示符。

   ```console
   shutdown -r -t 0 
   ```

## <a name="span-idtroubleshootingtipsspanspan-idtroubleshootingtipsspantroubleshooting-tips"></a><span id="troubleshooting_tips"></span><span id="TROUBLESHOOTING_TIPS"></span>故障排除提示

**调试应用程序必须允许通过防火墙**

调试器必须具有通过防火墙进行访问。 使用控制面板以允许通过防火墙进行访问。 

1. 打开**Control Panel&gt;系统和安全**然后单击**允许通过 Windows 防火墙的应用程序**。 

2. 在应用程序列表中，找到*Windows GUI 符号调试器*并*Windows 内核调试程序*。 

3. 使用复选框以允许这些两个应用程序**所有这三个**通过防火墙的不同网络类型。 

4. 向下滚动并单击**确定**，若要保存防火墙更改。 重新启动调试器。

    ![windows 控制显示所有三种网络类型启用了 Windows GUI 符号调试器和 Windows 内核调试器面板防火墙配置](images/firewall-control-pannel-windbg-gui-config.png)

**使用 Ping 测试连接性**

如果调试器超时，并且不会连接，使用在目标电脑上的 ping 命令来验证连接。 

   ```console
   C:\>Ping <HostComputerIPAddress> 
   ```

**选择用于网络调试的端口**

如果调试器超时，并且不会连接，则可能是因为已在使用默认端口号为 50000 或被阻止。 

您可以选择任意端口号从 49152 到 65535。 建议的范围是介于 50000 和 50039。 由调试器主机计算机上运行，将进行独占访问打开您选择的端口。 

**请注意**  可能通过公司的网络策略限制可用于网络调试的端口号的范围。 若要确定你公司的策略是否限制可以用于调试的网络端口的范围，请咨询网络管理员。

**支持的网络适配器**

如果"网络不支持调试任何在此计算机中的 Nic 上"将显示当您运行 kdnet.exe，它指的网络适配器不支持。 

主机计算机可以使用任何网络适配器，但在目标计算机必须使用的 Windows 调试工具支持的网络适配器。 有关支持的网络适配器的列表，请参阅[的 Windows 10 中的网络内核调试支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)和[对于 Windows 8.1 中的网络内核调试支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)。



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[支持的网络内核调试在 Windows 10 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)
 

[支持的网络内核调试在 Windows 8.1 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)


[KDNET 网络内核调试手动设置](setting-up-a-network-debugging-connection.md)


 







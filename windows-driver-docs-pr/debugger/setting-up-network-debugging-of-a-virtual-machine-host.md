---
title: 设置网络调试 KDNET 具有的虚拟机
description: 本主题介绍如何配置内核调试与 HYPER-V 虚拟机连接。
ms.assetid: E4C4D2A1-2FB0-4028-8A52-30B8F4F738D0
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5c42087cdf0cd516cb14cb57025a2697bbc8fe86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562172"
---
# <a name="setting-up-network-debugging-of-a-virtual-machine---kdnet"></a>设置网络调试的虚拟机-KDNET

本主题介绍如何配置与 HYPER-V 虚拟机 (VM) 的内核调试连接。


## <a name="hyper-v-virtual-machine-setup"></a>HYPER-V 虚拟机安装程序

若要调试 Gen 2 的 HYPER-V 虚拟机 (VM)，请完成以下步骤。

**1.使用 Windows 安装创建 VM**

有关如何创建 VM 的信息，请参阅[使用 HYPER-V 创建虚拟机](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)。

**2.定义外部虚拟交换机** 

若要与 VM 通信虚拟外部网络交换机可以使用。 有关如何创建外部网络交换机的信息，请参阅[创建虚拟网络](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)。

外部网络交换机配置时必须设置以下选项。

|选项| ReplTest1|
|----------|----------|
| 连接类型 | 外部网络|
| 允许管理操作系统共享此网络适配器 | 已启用 |
| VLAN ID | Disabled |


**3.禁用安全启动**

若要允许 kdnet 实用工具来更新 BCDEdit 启动设置，暂时通过执行以下步骤禁用安全启动虚拟机上。

1. 加载的 HYPER-V 管理器，并为 VM 选择的属性。

2. 单击**安全**设置。

3. 取消选中**启用安全启动**复选框。

4. 单击**确定**以保存设置。

您可以重新启用安全启动完成后，调试和您禁用了内核调试目标 VM 上。  


**4.安装用于 Windows 调试工具**

调试工具用于调试器和 kdnet 实用程序，并且必须安装。 有关如何下载和安装调试工具的信息，请参阅[的 Windows 中下载调试的工具](debugger-download-tools.md)。 


## <a name="setting-up-network-debugging-of-a-virtual-machine---kdnet"></a>设置网络调试的虚拟机-KDNET

### <a name="record-the-host-ip-address"></a>记录主机 IP 地址 

若要在目标虚拟机作为在同一台 PC 上运行主机调试，请按照下列步骤。 

1. 在主机计算机操作系统中，打开命令提示符窗口并输入*IPConfig*若要显示的 IP 配置。 

2. 在命令输出中，找到配置为外部虚拟交换机的以太网适配器。

    ```console
    ...

    Ethernet adapter vEthernet (External Virtual Switch):

    ...

    IPv4 Address. . . . . . . . . . . : <YourHostIPAddress>

    ...

    ```

3. 记下将用作调试主机地址的外部虚拟交换机的 IPv4 地址。

4. 若要确认目标和主机计算机之间的连接，请打开目标计算机上的提升的命令提示符窗口并输入以下命令，其中*YourHostIPAddress*是主计算机的 IP 地址。 

    ```console
    ping -4 <YourHostIPAddress>
    ```


## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-vm-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>设置 VM 的目标计算机

使用 kdnet.exe 实用程序自动配置调试器设置目标 PC 上，通过执行以下步骤。

1. 找到 WDK *kdnet.exe*并*VerifiedNICList.xml*文件。 默认情况下它们位于此处。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
```

> [!NOTE]
> 这些说明假定这两台 Pc 上的目标和主机运行 Windows 的 64 位版本。 如果这不是这样，最好的方法是运行在目标主机上运行工具的同一"位数"。 例如，如果目标正在运行 32 位 Windows，请在主机上运行 32 版本的调试器。 有关详细信息，请参阅[选择 32 位或 64 位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。
> 

4. 若要允许用于剪切和粘贴的长密钥，请启用增强的会话支持。 在虚拟机窗口中，从**视图**展开下拉列表菜单中，启用*增强会话*。 

5. 目标 VM 在计算机上，创建一个 C:\KDNET 目录并复制*kdnet.exe*并*VerifiedNICList.xml*文件复制到该目录。

6. 在目标计算机上，以管理员身份打开命令提示符窗口。 输入以下命令以验证目标计算机具有支持的网络适配器。

    ```console
    C:\KDNET>kdnet

    Network debugging is supported on the following NICs:
    busparams=0.25.0, Intel(R) 82579LM Gigabit Network Connection, KDNET is running on this NIC.kdnet.exe
    ```

7. 此命令设置主机系统的 IP 地址和生成的唯一连接密钥类型。 使用前面记录的主机系统的 IP 地址。  对于每个目标/主机对选取一个唯一的端口地址与在范围内 50000 50039，工作。 对于此示例中，我们将选择 50005。

    ```console
    C:\>kdnet <YourIPAddress> <YourDebugPort> 

    Enabling network debugging on Microsoft Hypervisor Virtual Machine.
    Key=3u8smyv477z20.2owh9gl90gbxx.3sfsihzgq7di4.nh8ugnmzb4l7

    To debug this vm, run the following command on your debugger host machine.
    windbg -k net:port=50005,key=3u8smyv477z20.2owh9gl90gbxx.3sfsihzgq7di4.nh8ugnmzb4l7

    Then restart this VM by running shutdown -r -t 0 from this command prompt.
    ```

8. 使用 CRTL + C 将提供的 windbg 输出复制到命令缓冲区。 执行此操作可避免尝试记下长的密钥值，则返回该值。

9. 完成后重新启用 BitLocker 和安全启动配置调试器设置。

10. 由于具有增强的会话支持的 VM 可以超时，当在断点处中断时，禁用*增强会话*支持使用**视图**展开下拉列表菜单在 VM 中。 

11. 加载并正在运行调试器后，将重启 VM。 接下来介绍了此过程。 


## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


2. 若要连接到目标 PC，使用 CTRL + V 粘贴主操作系统命令窗口中返回的 kdnet 之前复制的 windbg 字符串。

    ```console
    C:\Debuggers\windbg -k net:port=<YourDebugPort>,key=<YourKey> 
    ```

当首次尝试建立调试连接的网络时，你可能会提示您允许通过防火墙调试应用程序 （WinDbg 或 KD） 访问。 应通过检查对应的框来响应提示**所有这三个**网络类型： 域、 专用和公共。 



## <a name="span-idrestartingtargetspanspan-idrestartingtargetspanspan-idrestartingtargetspan-restarting-the-target-pc"></a><span id="Restarting_Target"></span><span id="restarting_target"></span><span id="RESTARTING_TARGET"></span> 重新启动目标 PC

调试器连接后，重新启动目标计算机。 若要强制完全重新启动 VM，请使用此命令中的，从管理员命令提示符。

   ```console
   shutdown -r -t 0 
   ```

目标虚拟机重新启动时，应连接的主机操作系统中的调试器。 

连接到 VM 后，命中时中断调试器，可以开始调试。 


## <a name="troubleshooting-kdnet-virtual-machine-network-debugging"></a>故障排除 KDNET 虚拟机网络调试 

如果调试器不会连接，则使用目标 VM 中的 ping 命令来验证连接。 

```console
C:\>Ping <HostComputerIPAddress> 
```

*权限无法正常工作，我不确定什么...* 

- 请确保你已通过你的防火墙让 WinDbg。 
- 确认使用 BCDEdit 或 kdnet 由生成的唯一密钥。


*我的 Vm 没有网络连接*  

- 从 Hyper-v 管理器中打开虚拟交换机管理器，选择你现有的虚拟交换机，并通过从下拉列表框中选择它，然后在虚拟交换机管理器对话框中单击确定更改为 Microsoft 内核调试网络适配器的外部网络 NIC框。  更新虚拟交换机 NIC 后, 确保然后关闭并重新启动 Vm。 



## <a name="sequence-to-add-hyper-v-role-to-a-windows-pc"></a>序列以将 HYPER-V 角色添加到 Windows PC

如果目标计算机是虚拟机主机，可以设置网络调试并仍然可以为虚拟机的网络访问。

假设你想要设置网络在以下情况中进行调试。

-   目标计算机具有单个网络接口卡。
-   要在目标计算机上安装 HYPER-V 角色。
-   想要在目标计算机上创建一个或多个虚拟机。

最佳方法是设置调试目标计算机上安装 HYPER-V 角色之前的网络。 然后虚拟机将具有网络访问权限。

如果决定设置网络调试目标计算机上安装 HYPER-V 角色后，必须更改要到 Microsoft 内核调试的网卡桥接各虚拟机的网络设置。 否则，虚拟机将不具有网络访问权限。


## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[设置内核模式调试的虚拟机手动使用虚拟 COM 端口](attaching-to-a-virtual-machine--kernel-mode-.md)

[手动设置的网络连接](setting-up-a-network-debugging-connection.md)

 

 







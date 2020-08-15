---
title: 使用 KDNET 设置虚拟机的网络调试
description: 本主题介绍如何配置与 Hyper-v 虚拟机的内核调试连接。
ms.assetid: E4C4D2A1-2FB0-4028-8A52-30B8F4F738D0
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3ed124f97b37cef2fcca3043924327000cdd903f
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253033"
---
# <a name="setting-up-network-debugging-of-a-virtual-machine---kdnet"></a>设置虚拟机的网络调试-KDNET

本主题介绍如何配置与 Hyper-v 虚拟机 (VM) 的内核调试连接。


## <a name="hyper-v-virtual-machine-setup"></a>Hyper-v 虚拟机安装程序

要 (VM 调试第2代 Hyper-v 虚拟机) 完成以下步骤。

**1. 创建已安装 Windows 的 VM**

有关如何创建 VM 的信息，请参阅 [使用 Hyper-v 创建虚拟机](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)。

**2. 定义外部虚拟交换机** 

若要与 VM 通信，可以使用虚拟外部网络交换机。 有关如何创建外部网络交换机的信息，请参阅 [创建虚拟网络](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)。

配置外部网络交换机时，必须设置以下选项。

|选项| 值|
|----------|----------|
| 连接类型 | 外部网络|
| 允许管理操作系统共享此网络适配器 | 已启用 |
| VLAN ID | 已禁用 |


**3. 禁用安全启动**

若要允许 kdnet 实用工具更新 BCDEdit boot 设置，请按照以下步骤在虚拟机上暂时禁用安全启动。

1. 加载 Hyper-v 管理器并选择 VM 的属性。

2. 选择 " **安全** 设置"。

3. 取消选中 " **启用安全启动** " 复选框。

4. 选择“确定”以保存设置。

完成调试并在目标 VM 上禁用内核调试之后，可以重新启用安全启动。  


**4. 安装适用于 Windows 的调试工具**

调试工具用于调试器和 kdnet 实用程序，并且必须安装。 有关如何下载和安装调试工具的信息，请参阅 [下载适用于 Windows 的调试工具](debugger-download-tools.md)。 


## <a name="setting-up-network-debugging-of-a-virtual-machine---kdnet"></a>设置虚拟机的网络调试-KDNET

### <a name="record-the-host-ip-address"></a>记录主机 IP 地址 

若要在目标虚拟机所在的同一台计算机上运行主机调试器，请执行以下步骤。 

1. 在主计算机操作系统中，打开命令提示符窗口并输入 *IPConfig* 以显示 IP 配置。 

2. 在命令输出中，找到配置为外部虚拟交换机的以太网适配器。

    ```console
    ...

    Ethernet adapter vEthernet (External Virtual Switch):

    ...

    IPv4 Address. . . . . . . . . . . : <YourHostIPAddress>

    ...

    ```

3. 记录外部虚拟交换机的 IPv4 地址，该地址将用作调试的主机地址。

4. 若要确认目标与主计算机之间的连接，请在目标计算机上打开提升的命令提示符窗口，然后输入以下命令，其中 *YourHostIPAddress* 是主计算机的 IP 地址。 

    ```console
    ping -4 <YourHostIPAddress>
    ```


## <a name="span-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspansetting-up-the-vm-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>设置 VM 目标计算机

按照以下步骤，使用 kdnet.exe 实用程序在目标电脑上自动配置调试器设置。

1. 找到 WDK *kdnet.exe* 和 *VerifiedNICList.xml* 文件。 默认情况下，它们位于此处。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
```

> [!NOTE]
> 这些说明假定两台 Pc 同时在目标和主机上运行64位版本的 Windows。 如果不是这种情况，最好的方法是在目标正在运行的主机上运行相同的工具 "位数"。 例如，如果目标运行的是32位 Windows，请在主机上运行调试器的32版本。 有关详细信息，请参阅 [选择32位或64位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。
> 

4. 若要允许使用剪切和粘贴的长密钥，请启用增强的会话支持。 在 "VM" 窗口的 " **查看** " 下拉菜单中，启用 " *增强会话*"。 

5. 在目标 VM 计算机上，创建一个 C:\KDNET 目录，并将 *kdnet.exe* 和 *VerifiedNICList.xml* 文件复制到该目录。

6. 在目标计算机上，以管理员身份打开“命令提示符”窗口。 输入此命令以验证目标计算机是否具有支持的网络适配器。

    ```console
    C:\KDNET>kdnet

    Network debugging is supported on the following NICs:
    busparams=0.25.0, Intel(R) 82579LM Gigabit Network Connection, KDNET is running on this NIC.kdnet.exe
    ```

7. 键入此命令可设置主机系统的 IP 地址并生成唯一的连接密钥。 使用之前记录的主机系统的 IP 地址。  为使用的每个目标/主机对选择唯一的端口地址，范围为50000-50039。 对于此示例，我们将选择50005。

    ```console
    C:\>kdnet <YourIPAddress> <YourDebugPort> 

    Enabling network debugging on Microsoft Hypervisor Virtual Machine.
    Key=3u8smyv477z20.2owh9gl90gbxx.3sfsihzgq7di4.nh8ugnmzb4l7

    To debug this vm, run the following command on your debugger host machine.
    windbg -k net:port=50005,key=3u8smyv477z20.2owh9gl90gbxx.3sfsihzgq7di4.nh8ugnmzb4l7

    Then restart this VM by running shutdown -r -t 0 from this command prompt.
    ```

8. 使用 CRTL + C 将提供的 windbg 输出复制到命令缓冲区中。 这样做可以避免尝试记下返回的长整型值。

9. 完成配置调试器设置后，重新启用 BitLocker 和安全启动。

10. 由于具有增强会话支持的 VM 在断点留在断点时可能会超时，因此请使用 VM 中的 "**查看**" 下拉菜单禁用*增强会话*支持。 

11. 加载并运行调试器后，将重新启动 VM。 下一步将介绍此过程。 


## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


2. 若要连接到目标 PC，请使用 CTRL + V 在主 OS 命令窗口中粘贴先前复制的 kdnet 返回的 windbg 字符串。

    ```console
    C:\Debuggers\windbg -k net:port=<YourDebugPort>,key=<YourKey> 
    ```

当你首次尝试建立网络调试连接时，系统可能会提示你允许调试应用程序 (WinDbg 或 KD) 通过防火墙进行访问。 你应通过选中 **所有三个** 网络类型（"域"、"专用" 和 "公共"）的框来响应提示。 



## <a name="span-idrestarting_targetspanspan-idrestarting_targetspanspan-idrestarting_targetspan-restarting-the-target-pc"></a><span id="Restarting_Target"></span><span id="restarting_target"></span><span id="RESTARTING_TARGET"></span> 重新启动目标 PC

连接调试器后，请重新启动目标计算机。 若要强制 VM 完全重新启动，请在管理员的命令提示符下使用此命令。

   ```console
   shutdown -r -t 0 
   ```

当目标虚拟机重新启动时，主机操作系统中的调试器应连接。 

连接到 VM 后，请在调试器上中断，然后可以开始调试。 


## <a name="troubleshooting-kdnet-virtual-machine-network-debugging"></a>KDNET 虚拟机网络调试疑难解答 

如果调试器未连接，请使用目标 VM 中的 ping 命令验证连接性。 

```console
C:\>Ping <HostComputerIPAddress> 
```

*有些东西不起作用，我不确定 .。。* 

- 请确保已通过防火墙让 WinDbg 完成。 
- 确认你使用的是由 BCDEdit 或 kdnet 生成的唯一键。


*我的 Vm 没有网络连接*  

- 从 Hyper-v 管理器打开虚拟交换机管理器，选择现有的虚拟交换机，并通过从下拉框中选择 "确定"，然后在 "虚拟交换机管理器" 对话框中选择 "确定"，将外部网络 NIC 更改为 Microsoft 内核调试网络适配器。  更新虚拟交换机 NIC 后，请确保关闭并重新启动 Vm。 



## <a name="sequence-to-add-hyper-v-role-to-a-windows-pc"></a>将 Hyper-v 角色添加到 Windows PC 的顺序

如果目标计算机是虚拟主机，则可以设置网络调试，并且仍能对虚拟机进行网络访问。

假设你想要在以下情况下设置网络调试。

-   目标计算机有一个网络接口卡。
-   你打算在目标计算机上安装 Hyper-v 角色。
-   你打算在目标计算机上创建一个或多个虚拟机。

最好的方法是在安装 Hyper-v 角色之前在目标计算机上设置网络调试。 然后虚拟机将有权访问网络。

如果在目标计算机上安装了 Hyper-v 角色后决定设置网络调试，则必须更改虚拟机的网络设置，以将其桥接到 Microsoft 内核网络调试适配器。 否则，虚拟机将无法访问网络。


## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[使用虚拟 COM 端口手动设置虚拟机的内核模式调试](attaching-to-a-virtual-machine--kernel-mode-.md)

[手动设置网络连接](setting-up-a-network-debugging-connection.md)

 

 







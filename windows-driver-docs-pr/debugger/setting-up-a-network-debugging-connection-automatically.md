---
title: 自动设置 KDNET 网络内核调试
description: 使用 KDNET 为 Windows 调试工具自动配置网络内核调试。
keywords:
- 网络调试
- 以太网调试
- WinDbg
- KDNET
ms.date: 11/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: d45ae63d4ad1880092053fb7f1a44bacb6c8e14d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803617"
---
# <a name="setting-up-kdnet-network-kernel-debugging-automatically"></a>自动设置 KDNET 网络内核调试

适用于 Windows 的调试工具支持通过网络进行内核调试。 本主题介绍如何使用 kdnet.exe 安装工具自动设置网络调试。

运行调试器的计算机称为 *主机计算机*，被调试的计算机称为 *目标计算机*。 主计算机必须运行 Windows 7 或更高版本，并且目标计算机必须运行 Windows 8 或更高版本。

## <a name="determining-the-ip-address-of-the-host-computer"></a>确定主机计算机的 IP 地址

1. 确认目标和主机 Pc 已连接到网络集线器或使用适当的网络电缆进行切换。

2. 在主计算机上，打开命令提示符窗口并输入 *IPConfig* 以显示 IP 配置。

3. 在命令输出中，找到以太网适配器的 IPv4 地址。

```console
...

Ethernet adapter Ethernet:
...

IPv4 Address. . . . . . . . . . . : <YourHostIPAddress>
...

```

4. 记下要用于调试的网络适配器的 IPv4 地址。

## <a name="setting-up-the-host-and-target-computers"></a>设置主机和目标计算机

按照以下步骤，使用 kdnet.exe 实用程序在目标电脑上自动配置调试器设置。

1. 确认主机系统上已安装 Windows 调试工具。 有关下载和安装调试器工具的信息，请参阅 [下载适用于 Windows 的调试工具](debugger-download-tools.md)。 

2. 找到 *kdnet.exe* 和 *VerifiedNICList.xml* 文件。 默认情况下，它们位于此处。

   ```console
   C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
   ```

   > [!NOTE]
   > 这些说明假定两台 Pc 同时在目标和主机上运行64位版本的 Windows。 如果不是这种情况，最好的方法是在目标正在运行的主机上运行相同的工具 "位数"。 例如，如果目标运行的是32位 Windows，则在主机上运行调试器的32版本。 有关详细信息，请参阅 [选择32位或64位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。
   > 

3. 在主计算机上，将这两个文件复制到网络共享或拇指驱动器，以便在目标计算机上可用。

4. 在目标计算机上创建 C:\KDNET 目录，并将 *kdnet.exe* 和 *VerifiedNICList.xml* 文件复制到该目录。

   > [!IMPORTANT]
   > 在使用 kdnet.exe 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
   > 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。


5. 在目标计算机上，以管理员身份打开“命令提示符”窗口。 输入此命令以验证目标计算机是否具有支持的网络适配器。

   ```console
   C:\KDNET>kdnet.exe
   Network debugging is supported on the following NICs:
   busparams=1.0.0, Broadcom NetXtreme Gigabit Ethernet, Plugged in.  
   This Microsoft hypervisor supports using KDNET in guest VMs.
   ```

6. 由于 kdnet.exe 的输出指示支持目标上的网络适配器，因此可以继续。

7. 键入此命令可设置主机系统的 IP 地址并生成唯一的连接密钥。 使用主机系统的 IP 地址或名称。 在建议的50000-50039 范围内，为你使用的每个目标/主机对选择唯一的端口地址。

   ```console
   C:\>kdnet.exe <HostComputerIPAddress> <YourDebugPort> 
   
   Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
   Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
   ```

8. 将返回的密钥复制到 notepad.exe 文件中。

## <a name="connecting-windbg-to-the-target-for-kernel-debugging"></a>将 WinDbg 连接到用于内核调试的目标

在主计算机上，打开 WinDbg。 在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **网络** " 选项卡。将之前保存的端口号和密钥粘贴到前面的 notepad.exe 文件中。 选择“确定”。

你还可以通过打开命令提示符窗口并输入以下命令（其中 <YourPort> 是上面选择的端口）来启动 WinDbg 会话， <YourKey> 它是上面 kdnet.exe 返回的键。 将上保存的项粘贴到前面的 notepad.exe 文件中。

   ```console
  windbg -k -d net:port=<YourDebugPort>,key=<YourKey> 
   ```

示例中显示的可选-d 参数启用了中的早期中断。 有关详细信息，请参阅 [WinDbg Command-Line 选项](windbg-command-line-options.md)。

如果系统提示你允许 WinDbg 通过防火墙访问该端口，则允许 WinDbg 访问 **所有这三种** 不同网络类型的端口。

![windows 安全警报-windows 防火墙阻止了此应用的某些功能 ](images/debuglab-image-firewall-dialog-box.png)

此时，调试器将等待目标重新连接，并且与下面类似的文本将显示在调试器命令窗口中。

   ```console
   Microsoft (R) Windows Debugger Version 1.0.1908.30002 AMD64
   Copyright (c) Microsoft Corporation. All rights reserved.

   Using NET for debugging
   Opened WinSock 2.0
   Waiting to reconnect...
   ```

## <a name="restarting-the-target-pc"></a>重新启动目标 PC

调试器进入 "正在等待重新连接 ..."阶段，重新启动目标计算机。 重新启动计算机的一种方法是在管理员的命令提示符下使用此命令。

   ```console
   shutdown -r -t 0 
   ```

在目标计算机重新启动后，调试器应该会自动连接。

## <a name="troubleshooting-tips"></a>疑难解答指南

**必须通过防火墙允许调试应用程序**

调试器必须具有通过防火墙的访问权限。 使用 "控制面板" 允许通过防火墙进行访问。 

1. 打开 **"控制面板" " &gt; 系统和安全"** ，然后选择 " **允许应用通过 Windows 防火墙**"。 

2. 在应用程序列表中，找到 " *WINDOWS GUI 符号调试器* " 和 " *windows 内核调试器*"。 

3. 使用此复选框可允许这两个应用程序通过防火墙实现 **三** 种不同的网络类型。 

4. 向下滚动并选择 **"确定"** 以保存防火墙更改。 重启调试程序。

    ![windows 控制面板防火墙配置，其中显示已启用所有三种网络类型的 Windows GUI 符号调试器和 Windows 内核调试器](images/firewall-control-pannel-windbg-gui-config.png)

**使用 Ping 测试连接**

如果调试器超时且未连接，请使用目标电脑上的 ping 命令验证连接性。 

```console
   C:\>Ping <HostComputerIPAddress>
```

**选择用于网络调试的端口**

如果调试器超时且未连接，则可能是由于默认端口号50000已在使用或被阻止。 

你可以选择从49152到65535的任何端口号。 建议的范围介于50000和50039之间。 你选择的端口将打开，以供在主计算机上运行的调试器进行独占访问。 

**注意**  可用于网络调试的端口号范围可能受公司网络策略的限制。 若要确定公司的策略是否限制可用于网络调试的端口范围，请与网络管理员联系。

**支持的网络适配器**

如果在运行 kdnet.exe 时显示 "此计算机上的任何 Nic 不支持网络调试"，则表示不支持网络适配器。

主计算机可以使用任何网络适配器，但目标计算机必须使用 Windows 调试工具支持的网络适配器。 有关受支持的网络适配器的列表，请参阅在 [Windows 10 中为网络内核调试支持的以太网 nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md) 和 [Windows 8.1 中用于网络内核调试的受支持以太网 nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)。

## <a name="enable-additional-debugging-types"></a>启用其他调试类型

开始 Windows 10 10 月2020更新 (20H2) ，支持使用以下选项启用四种调试类型。

*b* -启用 bootmgr 调试。 有关详细信息，请参阅 [BCDEdit/bootdebug](/windows-hardware/drivers/devtest/bcdedit--bootdebug)。

*w* -启用 winload.exe 调试。 有关详细信息，请参阅 [BCDEdit/bootdebug](/windows-hardware/drivers/devtest/bcdedit--bootdebug)。

*h* -启用虚拟机监控程序调试。 有关详细信息，请参阅 [BCDEdit/hypervisorsettings](/windows-hardware/drivers/devtest/bcdedit--hypervisorsettings)。

*k* -启用内核调试。 有关详细信息，请参阅 [ (内核模式) 入门 ](getting-started-with-windbg--kernel-mode-.md)。

可以指定任意调试类型的组合。

如果未指定任何调试类型，则将启用内核调试。

如果虚拟机监控程序和内核调试都处于启用状态，则虚拟机监控程序端口将设置为值 port + 1。

### <a name="example-usage"></a>用法示例

使用-bkw 选项可以启用 bootmgr、内核和 winload.exe 调试。

```console
C:\>kdnet.exe <HostComputerIPAddress> <YourDebugPort> -bkw

Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

### <a name="summary-of-debugging-type-options"></a>调试类型选项摘要

| KNDET 选项 | 描述                  | 等效 set 命令           |
|--------------|------------------------------|----------------------------------|
| *b*          | 启用 bootmgr 调试    | bcdedit/bootdebug {bootmgr} on  |
| *h*          | 启用虚拟机监控程序调试 | bcdedit/set hypervisordebug on  |
| *k*          | 启用内核调试     | bcdedit/debug on                |
| *w*          | 启用 winload.exe 调试    | bcdedit/bootdebug on            |

## <a name="specify-bus-parameters"></a>指定总线参数

如果 kdnet 无法自动确定传输的总线参数，请使用此语法在命令行上使用/busparams 选项进行指定。

`kdnet.exe /busparams [b.d.f] [host] [port] [-[b][h][k][w]]`

[b. d. f] 指定要配置的设备的总线参数。

使用目标计算机上的设备管理器确定要用于调试的适配器的 PCI 总线、设备和功能号。 对于 "总线参数"，请输入 *b*。*d.**f* ，其中 *b*、 *d* 和 *f* 是适配器的总线号、设备号和功能号。 这些值显示在“常规”选项卡上的“位置”下的设备管理器中 。  

例如：

```console
C:\>kdnet.exe /busparams 0.29.7 <HostComputerIPAddress> <YourDebugPort> -bkw
```

## <a name="related-topics"></a>相关主题

[Windows 10 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

[Windows 8.1 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[手动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection.md)

[Getting Started with WinDbg (Kernel-Mode)](getting-started-with-windbg--kernel-mode-.md)（WinDbg 入门（内核模式））

[调试通用驱动程序 - 分步实验室（回显内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)

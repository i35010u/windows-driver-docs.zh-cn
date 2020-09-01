---
title: 手动设置 KDNET 网络内核调试
description: 适用于 Windows 的调试工具支持通过网络进行内核调试。
ms.assetid: B4A79B2E-D4B1-42CA-9121-DEC923C76927
keywords:
- 网络调试
- 以太网调试
- 扩展坞
- 通过网络电缆手动设置内核模式调试
ms.date: 12/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: cf0b370633d35f70bc7cb8755157383b53601ee4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210859"
---
# <a name="setting-up-kdnet-network-kernel-debugging-manually"></a>手动设置 KDNET 网络内核调试

适用于 Windows 的调试工具支持通过网络进行内核调试。 本主题介绍如何手动设置网络调试。

> [!IMPORTANT]
> 手动设置网络调试是一种复杂且容易出错的过程。
> 若要自动设置网络调试，请参阅 [自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。 **强烈**建议所有调试器用户使用 KDNET 实用程序。

运行调试器的计算机称为 *主机计算机*，被调试的计算机称为 *目标计算机*。 主计算机必须运行 Windows 7 或更高版本，并且目标计算机必须运行 Windows 8 或更高版本。

与使用其他类型的连接进行调试相比，通过网络进行调试具有以下优势。

- 主机和目标计算机可以位于本地网络上的任何位置。
- 可以轻松地从一台主机计算机调试多台目标计算机。
- 给定任意两台计算机，它们可能都有以太网适配器。 这种情况不太可能它们都具有串行端口，或者两者都具有1394端口。
- 网络调试比串行端口调试明显快。

## <a name="supported-network-adapters"></a>支持的网络适配器

主计算机可以使用任何网络适配器，但目标计算机必须使用 Windows 调试工具支持的网络适配器。 有关受支持的网络适配器的列表，请参阅在 [Windows 10 中为网络内核调试支持的以太网 nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md) 和 [Windows 8.1 中用于网络内核调试的受支持以太网 nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)。

## <a name="install-the-debugging-tools-for-windows"></a>安装适用于 Windows 的调试工具

确认主机系统上已安装适用于 Windows 的调试工具。 有关下载和安装调试器工具的信息，请参阅 [下载适用于 Windows 的调试工具](debugger-download-tools.md)。

## <a name="determining-the-ip-address-of-the-host-computer"></a>确定主机计算机的 IP 地址

使用以下过程之一确定主机的 IP 地址。

1. 在主计算机上，打开命令提示符窗口并输入以下命令：

   ```console
   ipconfig
   ```

    记下要用于调试的网络适配器的 IPv4 地址。

2. 在目标计算机上，打开命令提示符窗口并输入以下命令，其中 *YourIPAddress* 是主计算机的 IP 地址：

   ```console
   ping -4 <YourIPAddress>
   ```

## <a name="choosing-a-port-for-network-debugging"></a>选择用于网络调试的端口

选择将用于在主机和目标计算机上进行调试的端口号。 你可以选择从49152到65535的任何数字，建议的范围为 50000-50039。 你选择的端口将打开，以供在主计算机上运行的调试器进行独占访问。 请小心选择主机计算机上运行的任何其他应用程序未使用的端口号。

**注意**   可用于网络调试的端口号范围可能受公司网络策略的限制。 没有办法告诉主机计算机的限制。 若要确定公司的策略是否限制可用于网络调试的端口范围，请与网络管理员联系。

如果将多台目标计算机连接到一台主计算机，则每个连接必须具有唯一的端口号。 例如，如果将100目标计算机连接到一台主机计算机，则可将端口50000分配给第一个连接，将端口50001分配给第二个连接，将端口50002分配给第三个连接，依此类推。

**注意**   不同的主机可以使用相同的端口范围 (50000 到 50099) 来连接到另一个100目标计算机。

## <a name="setting-up-the-target-computer"></a>设置目标计算机

1. 验证目标计算机是否具有支持的网络适配器。 有关详细信息，请参阅以下主题。

    - [Windows 8.1 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

    - [Windows 10 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

2. 使用适当的网络电缆将支持的适配器连接到网络集线器或交换机。

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

3. 在提升的命令提示符窗口中，输入以下命令，其中 *w.x.y.z* 是主机计算机的 IP 地址， *n* 是你选择的端口号：

    ```console
    bcdedit /debug on

    bcdedit /dbgsettings net hostip:w.x.y.z port:n
    ```

4. **bcdedit** 将显示自动生成的键。 复制密钥，并将其存储在可移动存储设备（如 USB 闪存驱动器）上。 在主计算机上启动调试会话时，将需要此密钥。

    **注意**   强烈建议使用自动生成的密钥。 不过，你可以创建自己的密钥，如后面的 "创建自己的密钥" 部分所述。

5. 使用设备管理器确定要用于调试的适配器的 PCI 总线、设备和功能号。 这些值将显示在 "*常规*" 选项卡上的 "*位置*" 下设备管理器。 然后在提升的命令提示符窗口中输入以下命令，其中*b*、 *d*和*f*是适配器的总线号码、设备号和功能号：

    ```console
    bcdedit /set "{dbgsettings}" busparams b.d.f
    ```

6. 连接内核调试器后，将重新启动目标 PC。 这将在下一部分中介绍。

**注意**   如果要在目标计算机上安装 Hyper-v 角色，请参阅[设置虚拟机主机的网络调试](setting-up-network-debugging-of-a-virtual-machine-host.md)。

**警告**   如果目标计算机位于扩展坞，并且你为作为扩展坞一部分的网络适配器启用了网络调试，请不要从扩展坞中删除计算机。 如果需要从扩展坞中删除目标计算机，请先禁用内核调试。 若要在目标计算机上禁用内核调试，请以管理员身份打开 "命令提示符" 窗口，然后输入命令 " **bcdedit/debug off**"。 重新启动目标计算机。

## <a name="starting-the-debugging-session"></a>启动调试会话

确认主机计算机的网络适配器连接到网络集线器或使用适当的网络电缆进行切换。

在主计算机上，打开 WinDbg。 在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **网络** " 选项卡。输入端口号和密钥。 选择“确定”。

你还可以通过打开命令提示符窗口并输入以下命令（其中 *n* 是你的端口号，而 *MyKey* 是设置目标计算机时由 **bcdedit** 自动生成的密钥）来启动与 WinDbg 的会话：

```console
windbg -k net:port=<n>,key=<MyKey>
```

如果系统提示你允许 WinDbg 通过防火墙访问该端口，则允许 WinDbg 访问 **所有这三种** 不同网络类型的端口。

### <a name="using-kd"></a>使用 KD

在主计算机上，打开命令提示符窗口。 输入以下命令，其中 *n* 为端口号， *MyKey* 是设置目标计算机时由 **bcdedit** 自动生成的密钥：

```console
kd -k net:port=<n>,key=<MyKey>
```

如果系统提示你允许 WinDbg 通过防火墙访问该端口，则允许 WinDbg 访问 **所有这三种** 不同网络类型的端口。

## <a name="restarting-the-target-pc"></a>重新启动目标 PC

连接到调试器并等待连接后，请重新启动目标计算机。 重新启动 PC 的一种方法是在管理员的命令提示符下使用此命令。

   ```console
   shutdown -r -t 0
   ```

当目标重新启动时，主机操作系统中的调试器应连接。

连接到主机上的目标后，请在调试器上中断，然后可以开始调试。

### <a name="allowing-the-debugger-through-the-firewall"></a>允许调试器通过防火墙

当你首次尝试建立网络调试连接时，系统可能会提示你允许调试应用程序 (WinDbg 或 KD) 通过防火墙进行访问。 Windows 的客户端版本显示提示，但 Windows 的服务器版本不显示提示。 你应通过选中 **所有三个** 网络类型（"域"、"专用" 和 "公共"）的框来响应提示。 如果未收到提示，或在提示可用时未选中相应的复选框，则必须使用 "控制面板" 允许通过防火墙进行访问。 打开 **"控制面板" " &gt; 系统和安全"** ，然后选择 " **允许应用通过 Windows 防火墙**"。 在应用程序列表中，找到 "Windows GUI 符号调试器" 和 "Windows 内核调试器"。 使用此复选框可以通过防火墙允许这两个应用程序。  (WinDbg 或 KD) 重新启动调试应用程序。

## <a name="encryption-key"></a>加密密钥

为了保证目标计算机的安全，必须对在主机和目标计算机之间传送的数据包进行加密。 我们强烈建议你在将目标计算机配置) 时，使用由 **bcdedit** 提供 (自动生成的加密密钥。 网络调试使用指定为 4 64 位值（36以句点分隔）的256位密钥。 每个64位值都使用最多13个字符来指定。 有效字符是从 a 到 z 的字母和数字0到9的数字。 不允许使用特殊字符。

若要指定您自己的密钥，请在目标计算机上打开提升的命令提示符窗口。 输入以下命令，其中， *w.x.y.z* 是主计算机的 IP 地址， *n* 是你的端口号， *密钥* 是你的密钥：

```console
bcdedit /dbgsettings net hostip:w.x.y.z port:n key:Key
```

更改 dbgsettings 时，需要重新启动目标计算机。

## <a name="troubleshooting-tips"></a>故障排查提示

### <a name="debugging-application-must-be-allowed-through-firewall"></a>必须通过防火墙允许调试应用程序

当你首次尝试建立网络调试连接时，系统可能会提示你允许调试应用程序 (WinDbg 或 KD) 通过防火墙进行访问。 Windows 的客户端版本显示提示，但 Windows 的服务器版本不显示提示。 你应通过选中 **所有三个** 网络类型（"域"、"专用" 和 "公共"）的框来响应提示。 如果未收到提示，或在提示可用时未选中相应的复选框，则必须使用 "控制面板" 允许通过防火墙进行访问。 打开 **"控制面板" " &gt; 系统和安全"** ，然后选择 " **允许应用通过 Windows 防火墙**"。 在应用程序列表中，找到 " *WINDOWS GUI 符号调试器* " 和 " *windows 内核调试器*"。 使用此复选框可以通过防火墙允许这两个应用程序。 向下滚动并选择 **"确定"** 以保存防火墙更改。 重启调试程序。

### <a name="port-number-must-be-in-range-allowed-by-network-policy"></a>端口号必须在网络策略允许的范围内

可用于网络调试的端口号范围可能受公司网络策略的限制。 若要确定公司的策略是否限制可用于网络调试的端口范围，请与网络管理员联系。 在目标计算机上，以管理员身份打开命令提示符窗口，然后输入命令 **bcdedit/dbgsettings**。 输出将与此类似。

```console
C:\> bcdedit /dbgsettings
key                     XXXXXX.XXXXX.XXXXX.XXXXX
debugtype               NET
hostip                  169.168.1.1
port                    50085
dhcp                    Yes
The operation completed successfully.
```

在上面的输出中，端口的值为50085。 如果 "端口" 的值超出了网络管理员允许的范围，请输入以下命令，其中 *w.x.y.z* 是主机计算机的 IP 地址， *YourDebugPort* 是允许范围中的端口号。

```console
bcdedit /dbgsettings net hostip:w.x.y.z port:YourDebugPort
```

更改目标计算机调试器设置后，请在主计算机上用新端口设置重新运行调试器，然后重新启动目标计算机。

### <a name="use-ping-to-test-connectivity"></a>使用 Ping 测试连接

如果调试器未连接，则在目标电脑上使用 ping 命令验证连接性。

   ```console
   C:\>Ping <HostComputerIPAddress>
   ```

请注意，如果您的主计算机未配置为在网络上是可发现的，则这可能不起作用，因为防火墙可能会阻止 ping 请求，因此，当您 ping 主机时，您不会收到任何响应。


### <a name="how-the-debugger-obtains-an-ip-address-for-the-target-computer"></a>调试器如何获取目标计算机的 IP 地址

目标计算机上的 KDNET 尝试使用动态主机配置协议 (DHCP) 为用于调试的网络适配器获取可路由的 IP 地址。 如果 KDNET 获取 DHCP 分配的地址，则目标计算机可由位于网络上任何位置的主机进行调试。 如果 KDNET 未能获取 DHCP 分配的地址，它将使用自动专用 IP 寻址 (APIPA) 来获取本地链接 IP 地址。 本地链接 IP 地址不可路由，因此主机和目标不能使用本地链接 IP 地址通过路由器进行通信。 在这种情况下，如果将主机和目标计算机插入到相同的网络集线器或交换机，则网络调试将起作用。

### <a name="always-specify-busparams-when-setting-up-kdnet-on-a-physical-machine-with-a-pci-based-nic"></a>在使用基于 PCI 的 NIC 的物理计算机上设置 KDNET 时，始终指定 busparams

如果要在使用基于 PCI 或 PCIe 的 NIC 的物理计算机上设置 KDNET，应始终为要用于 KDNET 的 NIC 指定 busparams。 若要指定总线参数，请打开设备管理器，然后找到要用于调试的网络适配器。 打开网络适配器的属性页，并记下 "*常规*" 选项卡上 "*位置*" 下显示的 "总线号码"、"设备编号" 和 "功能编号"。在提升的命令提示符窗口中，输入以下命令，其中*b*、 *d*和*f*是以十进制格式表示的总线、设备和函数编号：

```console
bcdedit /set "{dbgsettings}" busparams b.d.f
```

如果调试器正在主机上运行，并等待连接，请使用此命令重新启动目标计算机。

```console
shutdown -r -t 0
```

## <a name="manually-delete-bcdedit-entries"></a>手动删除 BCDEdit 条目

通常不需要手动删除，但此处提供的是针对异常情况的故障排除过程。

使用 kdnet 实用程序时，不需要手动删除条目。 有关详细信息，请参阅 [自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。

使用 bcdedit – deletevalue 时，必须提供有效的 bcd 元素名称。 有关详细信息，请参阅 [BCDEdit/deletevalue](../devtest/bcdedit--deletevalue.md)。

若要手动删除 BCDEdit 条目，请完成以下步骤。

1. 在目标计算机上，以管理员身份打开“命令提示符”窗口。

2. 例如，输入此命令可删除主机 IP 地址的 BCDEdit 调试条目。

    ```console
    bcdedit -deletevalue {dbgsettings} hostip
    ```

删除 hostip 时，需要在调试程序命令行中指定 *target =* 。

3. 作为另一个示例，请使用此命令删除此端口条目。

    ```console
    bcdedit -deletevalue {dbgsettings} port
    ```

删除此端口条目时，KDNET 将使用默认的 ICANN 注册调试器端口5364。

## <a name="hyper-v"></a>Hyper-V

### <a name="setting-up-hyper-v"></a>设置 Hyper-V

如果要在目标计算机上安装 Hyper-v 角色，请参阅 [设置虚拟机主机的网络调试](setting-up-network-debugging-of-a-virtual-machine-host.md)。

有关 (VM) 调试 hyper-v 虚拟机的信息，请参阅 [设置虚拟机的网络调试 KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)。

### <a name="enabling-kdnet-on-a-hyper-v-host-that-is-running-vms-with-external-network-connectivity"></a>在运行具有外部网络连接的 Vm 的 hyper-v 主机上启用 KDNET

存在特定情况，这种情况并不常见，这会导致 Vm 中的网络停止工作：

- 已在电脑上启用 hyper-v，已创建外部网络交换机，并将其指向计算机中的物理 NIC，并且 Vm 已配置为使用该外部交换机进行网络连接。

- 然后，使用外部网络交换机指向的相同物理 NIC 在 hyper-v 主机操作系统上启用 KDNET，并重新启动主机。

- 使用之前配置的外部交换机的所有 Vm 在重启后将失去其网络连接。

这是设计使然，并且发生的原因是 KDNET 对其配置为使用的 NIC 进行独占控制，操作系统不加载该 NIC 的本机 NDIS 微型端口。  出现这种情况时，外部网络交换机不能再与本机 NDIS 微型端口驱动程序通信，并将停止工作。  若要解决此问题，请执行以下操作：

1.  从 Hyper-v 管理器打开虚拟交换机管理器，选择现有的虚拟交换机，并通过从下拉框中选择 "确定"，然后在 "虚拟交换机管理器" 对话框中选择 "确定"，将外部网络 NIC 更改为 *Microsoft 内核调试网络适配器* 。

2.  更新虚拟交换机 NIC 后，请关闭并重新启动 Vm。

关闭 KDNET 调试时，需要遵循相同的过程将外部交换机 repoint 回 NIC 的本机 NDIS 小型端口。  否则，在禁用调试后重新启动计算机时，将丢失 VM 连接。


## <a name="span-idipv6spanspan-idipv6spanspan-idipv6spanipv6"></a><span id="IPV6"></span><span id="ipv6"></span><span id="IPv6"></span>IPv6

Windows 版本1809中添加了 IPv6 支持。

若要在调试器中使用 IPv6，请完成这些步骤。

1. Ping \<debughostname\> ，并记下从输出行的回复报告的 IPv6 地址。使用此 IPv6 地址代替 x:y： z:p： d:q： r:n。

2. 使用 BCDEdit 删除 dbgsettings 中的任何现有 ip 地址值。

    ```console
    bcdedit -deletevalue {dbgsettings} hostip
    ```

3. 设置主机的 IPv6 地址。 字符串中不得有空格 `hostipv6=s:t:u:v:w:x:y:z` 。 <YourPort> 是要用于此目标计算机的网络端口号， \<YourKey\> 是四个部分的安全密钥， \<b.d.f\> 是要用于 KDNET 的 NIC 的总线设备功能位置编号。

    ```console
    bcdedit /dbgsettings net hostipv6:s:t:u:v:w:x:y:z port:<YourPort> key:<YourKey> busparams:<b.d.f>
    ```

4. 键入以下命令以确认 dbgsettings 设置正确。

    ```console
    C:\> bcdedit /dbgsettings
    busparams               0.25.0
    key                     2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
    debugtype               NET
    hostipv6                  2001:db8:0:0:ff00:0:42:8329
    port                    50010
    dhcp                    Yes
    The operation completed successfully.
    ```

5. 在主计算机上，使用此命令来启动调试器。 

    ```console
    Windbg -k net:port=<yournetworkportnumber>,key=<key_output_from_kdnet>,target=::<YourIPv6Address> 
    ```

6. 如果调试器正在主机上运行，并且等待连接，请重新启动目标计算机。 

7. 调试器应在启动过程中及早连接到主机调试器。 你将知道，KDNET 正在使用 IPv6 连接，因为在连接的消息中报告的 IP 地址将是 IPv6 地址，而不是 IPv4 地址。 

**说明**

- 允许指定 hostip 的每个调试器 bcd 设置都有相应的 hostipv6 元素。  有三个。  

    IPv4 | IPv6 | 使用情况
    |-----------|-----------|-----------|
    hostip | hostipv6 | 对于启动和内核调试
    targethostip | targethostipv6  | 特定于内核调试  
    hypervisorhostip | hypervisorhostipv6  | 对于 hyper-v 调试

- 如果为这两种调试类型中的任何一种设置了 hostipv6 样式地址，则表示你需要并且将获得 IPv6。

- 如果为这两种调试类型中的任何一种设置了 hostip 样式地址，则表示你需要并且将获得 IPv4。

- 目标将只执行 IPv4 或 IPv6，而不是同时执行这两个操作。 使用哪个版本的 IP 协议由目标计算机 dbgsettings 控制。  如果设置了 hostip，则目标将使用 IPv4。  如果设置了 hostipv6，则目标将使用 IPv6。

- 主机调试器通常会自动选择使用 IPv4 或 IPv6。 默认情况下，调试器同时侦听 IPv4 套接字和 IPv6 套接字，并自动连接到目标计算机上的任何一个。

- 如果要在主机上强制使用 IPv6，但希望调试器侦听来自目标的连接，则可以将添加 `target=::` 到调试程序命令行。 ：：是0的 IPv6 地址。

- 如果要在主机上的调试器中强制执行 IPv4 调试，但希望调试器侦听来自目标的连接，则可以将添加 `target=0.0.0.0` 到调试器命令行。 0.0.0.0 是 IPv4 地址0。

- 如果在调试程序命令行中指定，target =，并使用计算机名称，则调试器会将该计算机名称转换为 IPv4 地址和 IPv6 地址，并将尝试同时连接两者。

- 如果在调试程序命令行中指定，target =，并使用 IP 地址，则如果 IP 地址包含 any：个字符，则调试器将假定它是 IPv6 地址，并将对该连接强制使用 IPv6。  如果 IP 地址包含任何。 个字符，则调试器将假定它是 IPv4 地址，并将对该连接强制使用 IPv4。

- 如果在目标上设置 IPv6，并强制在调试程序命令行上使用 IPv4，则不会获得连接。

- 如果在目标上设置 IPv4，并强制在调试程序命令行上使用 IPv6，则也不会获得连接。




## <a name="related-topics"></a>相关主题

[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)

[Windows 10 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

[Windows 8.1 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)
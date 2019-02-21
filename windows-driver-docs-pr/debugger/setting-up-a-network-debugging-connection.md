---
title: KDNET 网络内核调试手动设置
description: 调试工具的 Windows 支持通过网络内核调试。
ms.assetid: B4A79B2E-D4B1-42CA-9121-DEC923C76927
keywords:
- 网络调试
- 以太网调试
- 扩展坞
- 内核模式下通过网络电缆手动调试设置
ms.date: 12/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 79081114edf4e475df2fcf353851bfa12642a005
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521055"
---
# <a name="setting-up-kdnet-network-kernel-debugging-manually"></a>KDNET 网络内核调试手动设置

调试工具的 Windows 支持通过网络内核调试。 本主题介绍如何设置网络手动调试。

> [!IMPORTANT]
> 设置手动调试网络是一个复杂和错误容易过程。
> 若要设置网络自动调试，请参阅[设置向上 KDNET 网络内核调试自动](setting-up-a-network-debugging-connection-automatically.md)。 使用 KDNET 实用工具是**强**建议所有调试器的用户。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。 在主计算机必须运行 Windows 7 或更高版本，并在目标计算机必须运行 Windows 8 或更高版本。

调试在网络上具有以下优点相比于其他类型的连接调试。

- 在主机和目标计算机可以是本地网络上的任意位置。
- 很容易地调试从一台主机计算机的多个目标计算机。
- 给定任意两台计算机，则很可能具有，同时将以太网适配器。 它不太可能，因为它们都将拥有串行端口或者同时使用 1394年端口。
- 网络调试是明显快于调试串行端口。

## <a name="supported-network-adapters"></a>支持的网络适配器

主机计算机可以使用任何网络适配器，但在目标计算机必须使用的 Windows 调试工具支持的网络适配器。 有关支持的网络适配器的列表，请参阅[的 Windows 10 中的网络内核调试支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)和[对于 Windows 8.1 中的网络内核调试支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)。

## <a name="install-the-debugging-tools-for-windows"></a>安装用于 Windows 调试工具

确认主机系统上安装了调试工具的 Windows。 有关下载和安装调试器工具的信息，请参阅[的 Windows 中下载调试的工具](debugger-download-tools.md)。

## <a name="determining-the-ip-address-of-the-host-computer"></a>确定主机计算机的 IP 地址

使用以下过程之一来确定主机计算机的 IP 地址。

1. 主计算机上打开命令提示符窗口并输入以下命令：

   ```console
   ipconfig
   ```

    记下你想要用于调试的网络适配器的 IPv4 地址。

2. 在目标计算机上，打开命令提示符窗口并输入以下命令，其中*YourIPAddress*是主计算机的 IP 地址：

   ```console
   ping -4 <YourIPAddress>
   ```

## <a name="choosing-a-port-for-network-debugging"></a>选择用于网络调试的端口

选择将用于在主机和目标计算机上进行调试的端口号。 可以选择从 49152 到 65535 之间的任意数量，建议的范围为 50000 50039。 由调试器主机计算机上运行，将进行独占访问打开您选择的端口。 请务必选择不使用主机计算机上运行的任何其他应用程序的端口号。

**请注意**  可能通过公司的网络策略限制可用于网络调试的端口号的范围。 没有办法指示从主计算机的限制是什么。 若要确定你公司的策略是否限制可以用于调试的网络端口的范围，请咨询网络管理员。

如果多台目标计算机连接到单个主机计算机时，每个连接必须具有唯一的端口号。 例如，100 台目标计算机连接到单个主机计算机时，您可以将端口 50000 分配给第一个连接、 端口 50001 到第二个连接，端口 50002 到第三个连接，依次类推。

**请注意**  不同的主机计算机可以使用相同范围的端口 (通过 50099 50000) 连接到另一个 100 目标计算机。

## <a name="setting-up-the-target-computer"></a>在目标计算机上安装的设置

1. 验证目标计算机具有支持的网络适配器。 请参阅以下主题，获取详细信息。

    - [支持的网络内核调试在 Windows 8.1 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

    - [支持的网络内核调试在 Windows 10 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

2. 受支持的适配器连接到网络集线器或切换使用相应的网络电缆。

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。

3. 在提升的命令提示符窗口，输入以下命令，其中*w.x.y.z*是主计算机的 IP 地址和*n*是所选的端口号：

    ```console
    bcdedit /debug on

    bcdedit /dbgsettings net hostip:w.x.y.z port:n
    ```

4. **bcdedit**将显示自动生成的密钥。 复制密钥并将其存储在可移动存储设备上类似于 USB 闪存驱动器。 在主计算机上启动调试会话时，将需要密钥。

    **请注意**  我们强烈建议你使用自动生成的密钥。 但是，可以创建自己的密钥，如后面的"创建你自己的密钥"部分中所述。

5. 如果在目标计算机中有多个网络适配器，使用设备管理器确定 PCI 总线、 设备和函数编号，为你想要用于调试的适配器。 然后在提升的命令提示符窗口，输入以下命令，其中*b*， *d*，并*f*是总线数、 设备数量和适配器的函数数量：

    ```console
    bcdedit /set "{dbgsettings}" busparams b.d.f
    ```

6. 附加内核调试程序之后，将重新启动目标 PC。 这将在下一部分中介绍。

**请注意**  如果你想要在目标计算机上安装 HYPER-V 角色，请参阅[设置网络调试的虚拟机主机](setting-up-network-debugging-of-a-virtual-machine-host.md)。

**谨慎**  如果目标计算机在扩展坞，并且必须是扩展坞的一部分的网络适配器启用网络调试，请不要删除计算机从扩展坞。 如果你需要从扩展坞中删除目标计算机，禁用内核调试第一个。 若要禁用内核调试目标计算机上，打开管理员命令提示符窗口并输入命令**bcdedit /debug 关闭**。 重新启动目标计算机。

## <a name="starting-the-debugging-session"></a>启动调试会话

确认网络集线器或交换机使用相应的网络电缆的主机计算机的网络适配器。

在主计算机上打开 WinDbg。 上**文件**菜单中，选择**内核调试**。 在内核调试对话框中，打开**Net**选项卡。输入端口号和密钥。 单击“确定” 。

您还可以启动会话使用 WinDbg 通过打开命令提示符窗口并输入以下命令，其中*n*是端口号和*MyKey*是由自动生成的密钥**bcdedit**目标计算机的设置时：

```console
windbg -k net:port=<n>,key=<MyKey>
```

如果系统提示有关允许 WinDbg 能够通过防火墙访问端口，允许访问的端口的 WinDbg**所有这三个**的不同网络类型。

### <a name="using-kd"></a>使用 KD

在主计算机上打开命令提示符窗口。 输入以下命令，其中*n*是端口号和*MyKey*是自动生成的密钥**bcdedit**目标计算机的设置时：

```console
kd -k net:port=<n>,key=<MyKey>
```

如果系统提示有关允许 WinDbg 能够通过防火墙访问端口，允许访问的端口的 WinDbg**所有这三个**的不同网络类型。

## <a name="restarting-the-target-pc"></a>重新启动目标 PC

调试器已连接，并为正在等待连接、 重新启动目标计算机后。 不要重新启动 PC 的一种方法是使用此命令中的，从管理员命令提示符。

   ```console
   shutdown -r -t 0
   ```

重新启动目标时，应连接的主机操作系统中的调试器。

连接到主机上的目标后，命中时中断调试器，可以开始调试。

### <a name="allowing-the-debugger-through-the-firewall"></a>允许通过防火墙调试器

当首次尝试建立调试连接的网络时，你可能会提示您允许通过防火墙调试应用程序 （WinDbg 或 KD） 访问。 客户端版本的 Windows 显示提示，但服务器版本的 Windows 不显示提示。 应通过检查对应的框来响应提示**所有这三个**网络类型： 域、 专用和公共。 如果您不会收到提示时，或如果未选中对应的框提示时可用，则必须使用控制面板以允许通过防火墙进行访问。 打开**Control Panel&gt;系统和安全**然后单击**允许通过 Windows 防火墙的应用程序**。 在应用程序列表中，找到 Windows GUI 符号调试程序和 Windows 内核调试程序。 使用复选框以允许通过防火墙这些两个应用程序。 重新启动调试应用程序 （WinDbg 或 KD）。

## <a name="encryption-key"></a>加密密钥

若要使目标计算机安全，必须对不同主机和目标计算机之间移动的数据包进行加密。 我们强烈建议你使用自动生成的加密密钥 (由**bcdedit**配置目标计算机时)。 网络调试使用指定为四个 64 位值，在基本 36，用句点分隔的一个 256 位密钥。 使用最多 13 个字符，可指定每个 64 位值。 有效字符是字母 a 到 z 和 0 到 9 的数字。 不允许使用特殊字符。

若要指定自己的密钥，请打开提升的命令提示符窗口在目标计算机上。 输入以下命令，其中*w.x.y.z*是主计算机的 IP 地址和*n*是你的端口号，并*密钥*是你的密钥：

```console
bcdedit /dbgsettings net hostip:w.x.y.z port:n key:Key
```

需要随时更改 dbgsettings 重新启动目标计算机。

## <a name="troubleshooting-tips"></a>疑难解答提示

### <a name="debugging-application-must-be-allowed-through-firewall"></a>调试应用程序必须允许通过防火墙

当首次尝试建立调试连接的网络时，你可能会提示您允许通过防火墙调试应用程序 （WinDbg 或 KD） 访问。 客户端版本的 Windows 显示提示，但服务器版本的 Windows 不显示提示。 应通过检查对应的框来响应提示**所有这三个**网络类型： 域、 专用和公共。 如果您不会收到提示时，或如果未选中对应的框提示时可用，则必须使用控制面板以允许通过防火墙进行访问。 打开**Control Panel&gt;系统和安全**然后单击**允许通过 Windows 防火墙的应用程序**。 在应用程序列表中，找到*Windows GUI 符号调试器*并*Windows 内核调试程序*。 使用复选框以允许通过防火墙这些两个应用程序。 向下滚动并单击**确定**，若要保存防火墙更改。 重新启动调试器。

### <a name="port-number-must-be-in-range-allowed-by-network-policy"></a>端口号必须在范围内允许的网络策略

可能通过公司的网络策略限制可用于网络调试的端口号的范围。 若要确定你公司的策略是否限制可以用于调试的网络端口的范围，请咨询网络管理员联系。 在目标计算机上，打开管理员命令提示符窗口并输入命令**bcdedit /dbgsettings**。 输出将类似于此。

```console
C:\> bcdedit /dbgsettings
key                     XXXXXX.XXXXX.XXXXX.XXXXX
debugtype               NET
hostip                  169.168.1.1
port                    50085
dhcp                    Yes
The operation completed successfully.
```

在上面的输出端口的值是 50085。 如果端口的值位于由网络管理员允许的范围外，输入以下命令，其中*w.x.y.z*是主计算机的 IP 地址和*YourDebugPort*是中的端口号允许的范围。

```console
bcdedit /dbgsettings net hostip:w.x.y.z port:YourDebugPort
```

更改目标计算机调试程序设置之后, 重新运行主机上使用新的端口设置，调试器，然后重新启动目标计算机。

### <a name="use-ping-to-test-connectivity"></a>使用 Ping 测试连接性

如果调试器不会连接使用在目标电脑上的 ping 命令来验证连接。

   ```console
   C:\>Ping <HostComputerIPAddress>
   ```

请注意，这可能无法正常是否在主计算机未配置为在网络上发现的因为防火墙可能阻止 ping 请求，并正因为如此，则不会获得任何响应时成功进行 ping 操作主机。


### <a name="how-the-debugger-obtains-an-ip-address-for-the-target-computer"></a>调试器如何获取 IP 地址为目标计算机

在目标计算机上的 KDNET 尝试使用动态主机配置协议 (DHCP) 来获取的可路由的 IP 地址的正用于调试的网络适配器。 如果 KDNET 获取 DHCP 分配地址，则可以通过主机计算机位于网络上的任意位置调试目标计算机。 如果 KDNET 无法获取 DHCP 分配地址，它使用自动专用 IP 寻址 (APIPA) 来获取本地链路 IP 地址。 链接本地 IP 地址不是可路由，因此主机和目标不能使用本地链路 IP 地址通过路由器进行通信。 在这种情况下，在网络调试将工作，如果主机和目标将计算机插头插入到同一个网络集线器或交换机。

### <a name="always-specify-busparams-when-setting-up-kdnet-on-a-physical-machine-with-a-pci-based-nic"></a>PCI 的物理计算机上设置 KDNET 基于 NIC 时，始终指定 busparams

如果您设置了 KDNET PCI 的物理计算机上或 PCIe 基于 NIC，您应始终指定 busparams 想要用于 KDNET 的 nic。 若要指定总线参数，打开设备管理器，并找到你想要用于调试的网络适配器。 打开的网络适配器，属性页，并记下总线编号、 设备数量和函数编号。 在提升的命令提示符窗口，输入以下命令，其中*b*， *d*，并*f*是十进制格式的总线、 设备和函数编号：

```console
bcdedit /set "{dbgsettings}" busparams b.d.f
```

当调试器主机计算机上运行，等待连接，请重新启动目标计算机中，使用此命令。

```console
shutdown -r -t 0
```

## <a name="manually-delete-bcdedit-entries"></a>手动删除 BCDEdit 条目

手动删除不是通常情况下必需的但此处提供了在故障排除过程中的异常情况。

使用 kdnet 实用工具时，手动删除的项不需要。 有关详细信息，请参阅[设置向上 KDNET 网络内核调试自动](setting-up-a-network-debugging-connection-automatically.md)。

当使用 bcdedit – deletevalue 是，必须提供一个有效的 bcd 的元素名称。 有关详细信息，请参阅[BCDEdit /deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue)。

若要手动删除 BCDEdit 条目，请完成以下步骤。

1. 在目标计算机上，以管理员身份打开命令提示符窗口。

2. 例如，输入以下命令以删除调试主机 IP 地址条目 BCDEdit。

    ```console
    bcdedit -deletevalue {dbgsettings} hostip
    ```

删除主机时，需要指定*目标 =* 调试器命令行上。

3. 作为另一个示例中，删除将使用此命令的端口条目。

    ```console
    bcdedit -deletevalue {dbgsettings} port
    ```

当删除端口条目时，KDNET 将使用 5364 默认 ICANN 注册调试程序端口。

## <a name="hyper-v"></a>Hyper-V

### <a name="setting-up-hyper-v"></a>设置的 HYPER-V

如果你想要在目标计算机上安装 HYPER-V 角色，请参阅[设置网络调试的虚拟机主机](setting-up-network-debugging-of-a-virtual-machine-host.md)。

有关调试的 hyper-v 虚拟机 (VM) 的信息，请参阅[设置网络调试的虚拟机-KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)。

### <a name="enabling-kdnet-on-a-hyper-v-host-that-is-running-vms-with-external-network-connectivity"></a>使用外部网络连接运行 Vm 的 hyper-v 主机上启用 KDNET

没有特定的情况下，这并不少见，这将导致网络中虚拟机停止工作：

- 已在电脑上启用 HYPER-V、 外部网络交换机已创建并指向在计算机中，物理 NIC 和 Vm 已配置为其网络中使用该外部交换机。

- 上的 hyper-v 主机操作系统使用的相同的物理 NIC 指向的外部网络交换机，然后启用 KDNET 并重新启动主机。

- 在重新启动后丢失其网络连接性的所有 Vm 在使用以前配置的外部交换机。

这是设计使然，并发生异常的原因 KDNET 采用排他控制其配置为使用的 NIC 和本机 NDIS 微型端口 NIC 未加载操作系统。  此操作时，外部网络交换机不再能够与本机 NDIS 微型端口驱动程序，并将停止工作。  若要解决这种情况下，请执行以下操作：

1.  打开虚拟交换机管理器从 HYPER-V 管理器中，选择你的现有虚拟交换机和更改的外部网络 NIC *Microsoft 内核调试网络适配器*通过从下拉列表框中选择它，然后单击确定中虚拟交换机管理器对话框。

2.  更新虚拟交换机的 NIC、 关闭和重启后 Vm。

当 KDNET 调试处于关闭状态时，将需要相同的过程后跟 nic 重新定位外部切换回本机 NDIS 微型端口  否则禁用调试后重新启动计算机时，VM 连接性将会丢失。


## <a name="span-idipv6spanspan-idipv6spanspan-idipv6spanipv6"></a><span id="IPV6"></span><span id="ipv6"></span><span id="IPv6"></span>IPv6

Windows 版本 1809年添加了 IPv6 支持。

若要使用 IPv6 使用调试器，请完成这些步骤。

1. Ping 你\<debughostname\>和 IPv6 地址，请注意报告上输出行的回复。使用 x: y:z:p:d:q:r:n 下面代替此 IPv6 地址。

2. 使用 BCDEdit 删除 dbgsettings 中任何现有的 ip 地址值。

    ```console
    bcdedit -deletevalue {dbgsettings} hostip
    ```

3. 设置主机的 IPv6 地址。 不能在任何空格`hostipv6=s:t:u:v:w:x:y:z`字符串。 <YourPort> 是为要为此目标计算机，使用的网络端口号\<YourKey\>是由四部分构成的安全密钥，并\<b.d.f\>总线设备函数位置号是想要用于 KDNET 的 nic。

    ```console
    bcdedit /dbgsettings net hostipv6:s:t:u:v:w:x:y:z port:<YourPort> key:<YourKey> busparams:<b.d.f>
    ```

4. 键入以下命令以确认正确设置 dbgsettings。

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

5. 在主机上使用此命令以启动调试器。 

    ```console
    Windbg -k net:port=<yournetworkportnumber>,key=<key_output_from_kdnet>,target=::<YourIPv6Address> 
    ```

6. 当调试器主机计算机上运行，等待连接，请重新启动目标计算机。 

7. 尽早在启动过程中，调试程序应连接到主机调试器。 您将知道 KDNET 正在使用的 IPv6 连接，因为已连接的消息中报告的 IP 地址将是 IPv6 地址，而不是 IPv4 地址。 

**说明**

- Bcd 设置的允许主机以指定每个调试器具有相应的 hostipv6 元素。  有三个。  

    IPv4 | IPv6 | 用法
    |-----------|-----------|-----------|
    主机 | hostipv6 | 用于启动和内核调试
    targethostip | targethostipv6  | 特定于内核调试  
    hypervisorhostip | hypervisorhostipv6  | 用于调试的 hyper-v

- 如果任何这些类型的调试设置 hostipv6 样式地址，它表示您希望并将获得 IPv6。

- 如果任何这些类型的调试设置主机样式地址，它表示您希望并将获取 IPv4。

- IPv4 或 IPv6，不能同时在相同时，将只执行此目标。 由目标计算机 dbgsettings 控制使用的 IP 协议的版本。  如果设置主机，则目标将使用 IPv4。  如果设置 hostipv6，目标将使用 IPv6。

- 主机调试器通常会自动选择使用的 IPv4 或 IPv6。 默认情况下调试器侦听 IPv4 套接字和将 IPv6 套接字，并将自动连接到目标计算机的任何一个。

- 如果你想要在主机上强制使用 IPv6 在调试器中的，但希望调试器来侦听来自目标的连接，则您可以添加、`target=::`到调试器命令行。 :: 为 0 的 IPv6 地址。

- 如果你想要强制 IPv4 的主机上，在调试器中调试，但希望调试器来侦听来自目标的连接，则您可以添加、`target=0.0.0.0`到调试器命令行。 0.0.0.0 是为 0 的 IPv4 地址。

- 如果指定，目标 = 调试器命令行上并使用计算机名称，调试器会将该计算机名称转换为 IPv4 地址和 IPv6 地址，并将尝试同时连接。

- 如果指定，目标 = on 调试器命令行中，并使用一个 IP 地址，如果 IP 地址包含任何包含任何： 字符，调试器将假定它是 IPv6 地址，并将强制使用 IPv6，为该连接。  如果 IP 地址包含任何。 字符，调试器将假定它是 IPv4 地址，并将强制使用 IPv4，为该连接。

- 如果在目标上安装 IPv6 和调试器命令行上强制使用 IPv4 时，不会获得连接。

- 如果在目标上安装 IPv4 和调试器命令行上强制使用 IPv6，你也不会获得连接。




## <a name="related-topics"></a>相关主题

[KDNET 网络内核调试会自动设置](setting-up-a-network-debugging-connection-automatically.md)

[支持的网络内核调试在 Windows 10 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

[支持的网络内核调试在 Windows 8.1 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

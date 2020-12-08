---
title: 在 Visual Studio 中设置通过网线进行的内核模式调试
description: 你可以使用 Microsoft Visual Studio 通过以太网网络设置和执行内核模式调试。
keywords:
- visual studio 网络调试
- visual studio 的以太网调试
- 通过以太网 visual studio 调试
ms.date: 05/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 714a41b2f682e040ccb2306d7706927d27fd6f73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803613"
---
# <a name="setting-up-kernel-mode-debugging-over-a-network-cable-in-visual-studio"></a>在 Visual Studio 中设置通过网线进行的内核模式调试

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

你可以使用 Microsoft Visual Studio 通过以太网网络设置和执行内核模式调试。 若要将 Visual Studio 用于内核模式调试，你必须将 Windows 驱动程序工具包 (WDK) 与 Visual Studio 集成。 有关如何安装集成环境的信息，请参阅 [使用 Visual Studio 进行调试](debugging-using-visual-studio.md)。

作为使用 Visual Studio 设置以太网调试的替代方法，你可以自动执行安装。 有关详细信息，请参阅 [自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。

与使用其他类型的电缆进行调试相比，通过以太网网络进行调试具有以下优势：

-   主机和目标计算机可以位于本地网络上的任何位置。
-   可以轻松地从一台主机计算机调试多台目标计算机。
-   网络电缆价格低廉且随时可用。
-   给定任意两台计算机，它们可能都有以太网适配器。 这种情况不太可能它们都具有串行端口，或者两者都具有1394端口。

运行调试器的计算机称为 " *主机*"，正在调试的计算机称为 " *目标计算机*"。 主计算机必须运行 Windows XP 或更高版本，并且目标计算机必须运行 Windows 8 或更高版本。

## <a name="span-idsupported_network_adaptersspanspan-idsupported_network_adaptersspanspan-idsupported_network_adaptersspansupported-network-adapters"></a><span id="Supported_network_adapters"></span><span id="supported_network_adapters"></span><span id="SUPPORTED_NETWORK_ADAPTERS"></span>支持的网络适配器


主计算机可以使用任何有线或无线网络适配器，但目标计算机必须使用 Windows 调试工具支持的网络适配器。 若要查看受支持的网络适配器的列表，请参阅在[Windows 10 中为网络内核调试](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)提供支持的[用于网络内核调试的以太网 nic Windows 8.1](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)和。

## <a name="span-idconfiguring_the_host_and_target_computerspanspan-idconfiguring_the_host_and_target_computerspanspan-idconfiguring_the_host_and_target_computerspanconfiguring-the-host-and-target-computer"></a><span id="Configuring_the_host_and_target_computer"></span><span id="configuring_the_host_and_target_computer"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTER"></span>配置主机和目标计算机


1.  使用和适当的网络电缆将目标计算机的网络适配器连接到网络集线器或交换机。 将主计算机的网络适配器连接到网络集线器，或使用标准电缆或无线连接进行切换。
2.  按照为 [驱动程序部署设置计算机和测试 (WDK 8.1) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md)中所述，开始配置主机和目标计算机。
3.  在主计算机上，在 Visual Studio 的 "计算机配置" 对话框中，选择 " **设置计算机"，然后选择 "调试器设置**"。
4.  对于 " **连接类型**"，请选择 " **网络**"。

    ![屏幕截图显示了具有以下字段的值的调试器设置示例：连接类型、目标名称和总线参数](images/setupnetvs.png)

    对于 " **端口号**"，接受默认值或填写所选值。 你可以选择从49152到65535的任何数字。 你选择的端口将打开，以供在主计算机上运行的调试器进行独占访问。 请小心选择主机计算机上运行的任何其他应用程序未使用的端口号。

    **注意**  可用于网络调试的端口号范围可能受公司网络策略的限制。 没有办法告诉主机计算机的限制。 若要确定公司的策略是否限制可用于网络调试的端口范围，请与网络管理员联系。

    对于 **密钥**，我们强烈建议使用自动生成的默认值。 不过，如果愿意，也可以输入自己的密钥。 有关详细信息，请参阅本主题后面的 [创建自己的密钥](#creating-your-own-key) 。 对于 " **主机 IP**"，请接受默认值。 这是主计算机的 IP 地址。

    使用目标计算机上的设备管理器确定要用于调试的适配器的 PCI 总线、设备和功能号。 对于 "**总线参数**"，请输入 *b*。*d.**f* ，其中 *b*、 *d* 和 *f* 是适配器的总线号、设备号和功能号。 这些值显示在“常规”选项卡上的“位置”下的设备管理器中 。  

5.  配置过程需要几分钟的时间，并且可能会自动重启目标计算机一次或两次。 完成此过程后，单击 " **完成**"。

**警告**  如果目标计算机位于扩展坞，并且你为作为扩展坞一部分的网络适配器启用了网络调试，请不要从扩展坞中删除计算机。 如果需要从扩展坞中删除目标计算机，请先禁用内核调试。 若要在目标计算机上禁用内核调试，请以管理员身份打开 "命令提示符" 窗口，然后输入命令 " **bcdedit/debug off**"。 重新启动目标计算机。

 

**注意**  如果要在目标计算机上安装 Hyper-v 角色，请参阅 [设置虚拟机主机的网络调试](setting-up-network-debugging-of-a-virtual-machine-host.md)。

 

## <a name="span-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>验证目标计算机上的 dbgsettings

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

在目标计算机上，以管理员身份打开命令提示符窗口，然后输入以下命令：

**bcdedit/dbgsettings**

**bcdedit/enum**

```console
...
key                     RF8...KNE
debugtype               NET
hostip                  10.125.5.10
port                    50001
dhcp                    Yes
...
busparams               0.29.7
...
```

验证 *debugtype* 是 NET， *Port* 是在 Visual Studio 中的主计算机上指定的端口号。 此外，请确认 *密钥* 是 (自动生成的密钥，或者在 Visual Studio 中指定) 。

验证 *busparams* 是否与指定的总线参数匹配。

如果看不到为 **总线参数** 输入的值，请输入以下命令：

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**.**<em>d.</em>**.**<em>f</em>

其中， *b*、 *d* 和 *f* 是目标计算机上选择用于调试的网络适配器的总线、设备和功能号。 这些值显示在设备管理器的 "*常规*" 选项卡上的 "*位置*" 下。  

例如：

**bcdedit/set "{dbgsettings}" busparams 0.29。7**

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  在主计算机上，在 Visual Studio 的 " **工具** " 菜单中，选择 " **附加到进程**"。
2.  对于 " **传输**"，请选择 " **Windows 内核模式调试程序**"。
3.  对于 " **限定符**"，选择以前配置的目标计算机的名称。
4.  单击 **“附加”** 。

## <a name="span-idallowing_the_debugger_through_the_firewallspanspan-idallowing_the_debugger_through_the_firewallspanspan-idallowing_the_debugger_through_the_firewallspanallowing-the-debugger-through-the-firewall"></a><span id="Allowing_the_debugger_through_the_firewall"></span><span id="allowing_the_debugger_through_the_firewall"></span><span id="ALLOWING_THE_DEBUGGER_THROUGH_THE_FIREWALL"></span>允许调试器通过防火墙


当你首次尝试建立网络调试连接时，系统可能会提示你允许调试应用程序 (Microsoft Visual Studio 通过防火墙) 。 Windows 的客户端版本显示提示，但 Windows 的服务器版本不显示提示。 通过检查所有三个网络类型（"域"、"专用" 和 "公共"）的框来响应提示符。 如果未收到提示，或在提示可用时未选中相应的复选框，则必须使用 "控制面板" 允许通过防火墙进行访问。 打开 **"控制面板" " &gt; 系统和安全**"，然后单击 " **允许应用通过 Windows 防火墙**"。 在应用程序列表中，使用复选框允许 Visual Studio 通过防火墙。 重新启动 Visual Studio。

## <a name="span-idcreating-your-own-keyspanspan-idcreating-your-own-keyspancreating-your-own-key"></a><span id="creating-your-own-key"></span><span id="CREATING-YOUR-OWN-KEY"></span>创建自己的密钥


为了保证目标计算机的安全，必须对在主机和目标计算机之间传送的数据包进行加密。 我们强烈建议你在配置目标计算机) 时，使用 Visual Studio 配置向导) 提供的自动生成的加密密钥 (。 不过，您可以选择创建自己的密钥。 网络调试使用指定为 4 64 位值（36以句点分隔）的256位密钥。 每个64位值都使用最多13个字符来指定。 有效字符是从 a 到 z 的字母和数字0到9的数字。 不允许使用特殊字符。 下面的列表提供了有效 (的示例，但并不是强) 密钥：

-   1.2.3.4
-   abc. 123
-   不使用。

## <a name="span-idtroubleshooting_tips_for_debugging_over_a_network_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_network_cablespantroubleshooting-tips-for-debugging-over-a-network-cable"></a><span id="troubleshooting_tips_for_debugging_over_a_network_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_NETWORK_CABLE"></span>通过网络电缆进行调试的故障排除提示


### <a name="span-iddebugging_application_must_be_allowed_through_firewallspanspan-iddebugging_application_must_be_allowed_through_firewallspanspan-iddebugging_application_must_be_allowed_through_firewallspandebugging-application-must-be-allowed-through-firewall"></a><span id="Debugging_application_must_be_allowed_through_firewall"></span><span id="debugging_application_must_be_allowed_through_firewall"></span><span id="DEBUGGING_APPLICATION_MUST_BE_ALLOWED_THROUGH_FIREWALL"></span>必须通过防火墙允许调试应用程序

你的调试器 (WinDbg 或 KD) 必须具有通过防火墙的访问权限。 可以使用 "控制面板" 允许通过防火墙进行访问。 打开 **"控制面板" " &gt; 系统和安全**"，然后单击 " **允许应用通过 Windows 防火墙**"。 在应用程序列表中，使用复选框允许 Visual Studio 通过防火墙。 重新启动 Visual Studio。

### <a name="span-idport_number_must_be_in_range_allowed_by_network_policyspanspan-idport_number_must_be_in_range_allowed_by_network_policyspanspan-idport_number_must_be_in_range_allowed_by_network_policyspanport-number-must-be-in-range-allowed-by-network-policy"></a><span id="Port_number_must_be_in_range_allowed_by_network_policy"></span><span id="port_number_must_be_in_range_allowed_by_network_policy"></span><span id="PORT_NUMBER_MUST_BE_IN_RANGE_ALLOWED_BY_NETWORK_POLICY"></span>端口号必须在网络策略允许的范围内

可用于网络调试的端口号范围可能受公司网络策略的限制。 若要确定公司的策略是否限制可用于网络调试的端口范围，请与网络管理员联系。

如果需要更改端口号，请使用以下过程。

1.  在主计算机上，在 Visual Studio 的“驱动程序”  菜单中，选择“测试”&gt;“配置计算机”  。
2.  选择测试计算机的名称，然后单击 " **下一步**"。
3.  选择 " **设置计算机" 并选择 "调试器设置**"。 单击 **“下一步”** 。
4.  对于 " **端口号**"，请输入网络管理员允许的范围内的数字。 单击 **“下一步”** 。
5.  重新配置过程将花费几分钟时间，并自动重启目标计算机。 完成此过程后，单击 " **下一步** " 和 " **完成**"。

### <a name="specify-busparams"></a>指定 busparams

你必须指定要用于调试的网络适配器的总线、设备和功能号。 若要指定总线参数，请打开设备管理器，然后找到要用于调试的网络适配器。 打开网络适配器的属性页，并记下 "*常规*" 选项卡上 "*位置*" 下显示的 "总线编号"、"设备编号" 和 "功能编号"。在提升的命令提示符窗口中，输入以下命令，其中 *b*、 *d* 和 *f* 是以十进制格式表示的总线、设备和函数编号：

**bcdedit-设置 "{dbgsettings}" busparams** <em>b</em>**。**<em>d.</em>**.**<em>f</em>

重新启动目标计算机。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

[Windows 10 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

[Windows 8.1 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[Windows 8 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

 


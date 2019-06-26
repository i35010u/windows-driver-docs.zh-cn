---
title: 在 Visual Studio 中设置通过网线进行的内核模式调试
description: 可以使用 Microsoft Visual Studio 设置和执行通过以太网网络的内核模式调试。
ms.assetid: 4D442355-526A-4F39-8341-614BB7A41A3E
keywords:
- 网络调试 visual studio
- 以太网调试 visual studio
- 相较于以太网 visual studio 调试
ms.date: 05/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8420a344c8072411521aca2dd2f0c2476ab455aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366383"
---
# <a name="setting-up-kernel-mode-debugging-over-a-network-cable-in-visual-studio"></a>在 Visual Studio 中设置通过网线进行的内核模式调试

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

可以使用 Microsoft Visual Studio 设置和执行通过以太网网络的内核模式调试。 若要使用内核模式调试的 Visual Studio，必须具有 Windows Driver Kit (WDK) 与 Visual Studio 集成。 有关如何安装集成的环境的信息，请参阅[Windows 驱动程序开发](https://go.microsoft.com/fwlink/p?linkid=301383)。

使用 Visual Studio 来设置调试的以太网的替代方法，您还可以自动执行安装程序。 有关详细信息，请参阅[设置向上 KDNET 网络内核调试自动](setting-up-a-network-debugging-connection-automatically.md)。

通过以太网网络调试具有以下优点相比于其他类型的电缆调试：

-   在主机和目标计算机可以是本地网络上的任意位置。
-   很容易地调试从一台主机计算机的多个目标计算机。
-   网络电缆是成本较低，并且随时可用。
-   给定任意两台计算机，则很可能具有，同时将以太网适配器。 它不太可能，因为它们都将拥有串行端口或者同时使用 1394年端口。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。 在主计算机必须运行 Windows XP 或更高版本，并且目标计算机必须运行 Windows 8 或更高版本。

## <a name="span-idsupportednetworkadaptersspanspan-idsupportednetworkadaptersspanspan-idsupportednetworkadaptersspansupported-network-adapters"></a><span id="Supported_network_adapters"></span><span id="supported_network_adapters"></span><span id="SUPPORTED_NETWORK_ADAPTERS"></span>支持的网络适配器


主机计算机可以使用任何有线或无线网络适配器，但在目标计算机必须使用的 Windows 调试工具支持的网络适配器。 有关支持的网络适配器的列表，请参阅[为 Windows 8.1 中的网络内核调试支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)和[对于 Windows 10 中的网络内核调试支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)。

## <a name="span-idconfiguringthehostandtargetcomputerspanspan-idconfiguringthehostandtargetcomputerspanspan-idconfiguringthehostandtargetcomputerspanconfiguring-the-host-and-target-computer"></a><span id="Configuring_the_host_and_target_computer"></span><span id="configuring_the_host_and_target_computer"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTER"></span>配置主机和目标计算机


1.  将目标计算机的网络适配器连接到网络集线器或切换使用和相应的网络电缆。 将主机计算机的网络适配器连接到网络集线器或切换使用标准电缆或无线连接。
2.  开始配置主机和目标计算机中所述[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。
3.  主机计算机上，在 Visual Studio 中，当您转至计算机配置对话框中，选择**预配计算机，并选择调试器设置**。
4.  有关**连接类型**，选择**网络**。

    ![屏幕截图显示调试程序的示例具有以下字段的值的设置： 连接类型、 目标名称和总线参数](images/setupnetvs.png)

    有关**端口号**，接受默认值或所选的值填充。 您可以选择任意数量从 49152 到 65535。 由调试器主机计算机上运行，将进行独占访问打开您选择的端口。 请务必选择不使用主机计算机上运行的任何其他应用程序的端口号。

    **请注意**  可能通过公司的网络策略限制可用于网络调试的端口号的范围。 没有办法指示从主计算机的限制是什么。 若要确定你公司的策略是否限制可以用于调试的网络端口的范围，请咨询网络管理员。

    有关**密钥**，我们强烈建议你使用自动生成的默认值。 但是，如果您愿意可以输入自己的密钥。 有关详细信息，请参阅[创建你自己的密钥](#creating-your-own-key)本主题中更高版本。 有关**主机 IP**，接受默认值。 这是在主计算机的 IP 地址。

    如果目标计算机具有只有一个网络适配器，则可以保留**总线参数**为空。 如果目标计算机上多个网络适配器，请使用目标计算机上设备管理器来确定 PCI 总线、 设备和函数编号，为你想要用于调试的适配器。 有关**总线参数**，输入*b*。*d*。*f*其中*b*， *d*，并且*f*是总线数、 设备数量和适配器的函数数量。

5.  配置过程需要几分钟时间，并可能会自动重新启动目标计算机一次或两次。 该过程完成后，单击**完成**。

**谨慎**  如果目标计算机在扩展坞，并且必须是扩展坞的一部分的网络适配器启用网络调试，请不要删除计算机从扩展坞。 如果你需要从扩展坞中删除目标计算机，禁用内核调试第一个。 若要禁用内核调试目标计算机上，打开管理员命令提示符窗口并输入命令**bcdedit /debug 关闭**。 重新启动目标计算机。

 

**请注意**  如果你想要在目标计算机上安装 HYPER-V 角色，请参阅[设置网络调试的虚拟机主机](setting-up-network-debugging-of-a-virtual-machine-host.md)。

 

## <a name="span-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>验证目标计算机上的 dbgsettings

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。

在目标计算机上，打开命令提示符窗口，以管理员身份，并输入以下命令：

**bcdedit /dbgsettings**

**bcdedit /enum**

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

确认*debugtype*是 NET 和*端口*是你在 Visual Studio 中指定主计算机的端口号。 此外确认*密钥*是 Visual Studio 中自动生成的密钥 （或您指定）。

如果您输入**总线参数**在 Visual Studio 中，确认*busparams*您指定的总线参数匹配。

如果您看不到值为输入**总线参数**，输入以下命令：

**bcdedit /set "{dbgsettings}" busparams** <em>b</em> **.** <em>d</em> **.** <em>f</em>

其中*b*， *d*，并*f*是总线、 设备和已选择要用于调试的目标计算机上的网络适配器的函数数量。

例如：

**bcdedit /set "{dbgsettings}" busparams 0.29.7**

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  上，在 Visual Studio 中，主机计算机上**工具**菜单中，选择**附加到进程**。
2.  有关**传输**，选择**Windows 内核模式调试程序**。
3.  有关**限定符**，选择以前配置的目标计算机的名称。
4.  单击**附加**。

## <a name="span-idallowingthedebuggerthroughthefirewallspanspan-idallowingthedebuggerthroughthefirewallspanspan-idallowingthedebuggerthroughthefirewallspanallowing-the-debugger-through-the-firewall"></a><span id="Allowing_the_debugger_through_the_firewall"></span><span id="allowing_the_debugger_through_the_firewall"></span><span id="ALLOWING_THE_DEBUGGER_THROUGH_THE_FIREWALL"></span>允许通过防火墙调试器


当首次尝试建立调试连接的网络时，可能提示你允许调试应用程序 (Microsoft Visual Studio)，通过防火墙。 客户端版本的 Windows 显示提示，但服务器版本的 Windows 不显示提示。 通过选中框，适用于所有三个网络类型来响应提示： 域、 专用和公共。 如果您不会收到提示时，或如果未选中对应的框提示时可用，则必须使用控制面板以允许通过防火墙进行访问。 打开**Control Panel&gt;系统和安全**，然后单击**允许通过 Windows 防火墙的应用程序**。 在应用程序列表中，使用对应的复选框以允许通过防火墙的 Visual Studio。 重新启动 Visual Studio。

## <a name="span-idcreating-your-own-keyspanspan-idcreating-your-own-keyspancreating-your-own-key"></a><span id="creating-your-own-key"></span><span id="CREATING-YOUR-OWN-KEY"></span>创建你自己的密钥


若要使目标计算机安全，必须对不同主机和目标计算机之间移动的数据包进行加密。 我们强烈建议你使用自动生成的加密密钥 （由 Visual Studio 配置向导） 配置目标计算机时)。 但是，您可以选择创建自己的密钥。 网络调试使用指定为四个 64 位值，在基本 36，用句点分隔的一个 256 位密钥。 使用最多 13 个字符，可指定每个 64 位值。 有效字符是字母 a 到 z 和 0 到 9 的数字。 不允许使用特殊字符。 以下列表提供了的有效示例 （尽管不强） 密钥：

-   1.2.3.4
-   abc.123.def.456
-   dont.use.previous.keys

## <a name="span-idtroubleshootingtipsfordebuggingoveranetworkcablespanspan-idtroubleshootingtipsfordebuggingoveranetworkcablespantroubleshooting-tips-for-debugging-over-a-network-cable"></a><span id="troubleshooting_tips_for_debugging_over_a_network_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_NETWORK_CABLE"></span>通过网络电缆进行调试的故障排除提示


### <a name="span-iddebuggingapplicationmustbeallowedthroughfirewallspanspan-iddebuggingapplicationmustbeallowedthroughfirewallspanspan-iddebuggingapplicationmustbeallowedthroughfirewallspandebugging-application-must-be-allowed-through-firewall"></a><span id="Debugging_application_must_be_allowed_through_firewall"></span><span id="debugging_application_must_be_allowed_through_firewall"></span><span id="DEBUGGING_APPLICATION_MUST_BE_ALLOWED_THROUGH_FIREWALL"></span>调试应用程序必须允许通过防火墙

调试器 （WinDbg 或 KD） 必须具有通过防火墙进行访问。 可以使用控制面板以允许通过防火墙进行访问。 打开**Control Panel&gt;系统和安全**，然后单击**允许通过 Windows 防火墙的应用程序**。 在应用程序列表中，使用对应的复选框以允许通过防火墙的 Visual Studio。 重新启动 Visual Studio。

### <a name="span-idportnumbermustbeinrangeallowedbynetworkpolicyspanspan-idportnumbermustbeinrangeallowedbynetworkpolicyspanspan-idportnumbermustbeinrangeallowedbynetworkpolicyspanport-number-must-be-in-range-allowed-by-network-policy"></a><span id="Port_number_must_be_in_range_allowed_by_network_policy"></span><span id="port_number_must_be_in_range_allowed_by_network_policy"></span><span id="PORT_NUMBER_MUST_BE_IN_RANGE_ALLOWED_BY_NETWORK_POLICY"></span>端口号必须在范围内允许的网络策略

可能通过公司的网络策略限制可用于网络调试的端口号的范围。 若要确定你公司的策略是否限制可以用于调试的网络端口的范围，请咨询网络管理员联系。

如果需要更改端口号，请使用以下过程。

1.  在主计算机上，在 Visual Studio 的**驱动程序**菜单中，选择**测试 &gt; 配置计算机**。
2.  选择测试计算机的名称，然后单击**下一步**。
3.  选择**预配计算机，并选择调试器设置**。 单击“下一步”  。
4.  有关**端口号**，输入一个数字，是由网络管理员允许的范围中。 单击“下一步”  。
5.  重新配置过程需要几分钟，并会自动重启目标计算机。 该过程完成后，单击**下一步**并**完成**。

### <a name="span-idspecifybusparamsiftargetcomputerhasmultiplenetworkadaptersspanspan-idspecifybusparamsiftargetcomputerhasmultiplenetworkadaptersspanspan-idspecifybusparamsiftargetcomputerhasmultiplenetworkadaptersspanspecify-busparams-if-target-computer-has-multiple-network-adapters"></a><span id="Specify_busparams_if_target_computer_has_multiple_network_adapters"></span><span id="specify_busparams_if_target_computer_has_multiple_network_adapters"></span><span id="SPECIFY_BUSPARAMS_IF_TARGET_COMPUTER_HAS_MULTIPLE_NETWORK_ADAPTERS"></span>如果目标计算机具有多个网络适配器，指定 busparams

如果目标计算机具有多个网络适配器，必须指定总线、 设备和你想要用于调试的网络适配器的函数数量。 若要指定总线参数，请打开设备管理器，并找到你想要用于调试的网络适配器。 打开的网络适配器，属性页，并记下总线编号、 设备数量和函数编号。 在提升的命令提示符窗口，输入以下命令，其中*b*， *d*，并*f*是十进制格式的总线、 设备和函数编号：

**bcdedit -set "{dbgsettings}" busparams** <em>b</em> **.** <em>d</em> **.** <em>f</em>

重新启动目标计算机。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

[支持的网络内核调试在 Windows 10 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

[支持的网络内核调试在 Windows 8.1 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[支持的网络内核调试 Windows 8 中的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

 

 







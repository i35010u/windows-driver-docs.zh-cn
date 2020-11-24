---
title: 使用 KDNET 设置 ARM 设备上的 USB EEM 上的 Kernel-Mode 调试
description: 适用于 Windows 的调试工具支持使用 ARM 设备上的 EEM 通过 USB 电缆进行内核调试。 本主题介绍如何使用 kdnet.exe 实用程序在 ARM 设备上设置 USB EEM。
ms.assetid: 78D49BDA-BC49-4FF3-B66B-2F6C1C7C2D98
ms.date: 11/23/2020
ms.localizationpriority: medium
ms.openlocfilehash: 23498364d280d43157b2ebc2271b49ce80ccf3e9
ms.sourcegitcommit: 9e5ade5d1a311383016385ae3bc3f0a22da1dfc5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/24/2020
ms.locfileid: "95553288"
---
# <a name="setting-up-kernel-mode-debugging-over-usb-eem-on-an-arm-device-using-kdnet"></a>使用 KDNET 设置 ARM 设备上的 USB EEM 上的 Kernel-Mode 调试

适用于 Windows 的调试工具支持使用 ARM 设备上的 EEM 通过 USB 电缆进行内核调试。 本主题介绍如何使用 kdnet.exe 实用程序在 ARM 设备上设置 USB EEM。

运行调试器的计算机称为 *主机计算机*，被调试的计算机称为 *目标计算机*。

## <a name="kernel-mode-usb-eem-arm-device-requirements"></a>Kernel-Mode USB EEM ARM 设备要求

将需要以下项：

- 在目标计算机上，Synopsys USB 3.0 控制器连接到 USB 类型 C 端口。

- 在主计算机上，需要 USB 2.0 或 USB 3.0 端口。

- 若要将主机类型连接到目标类型 C 端口，需要使用标准 USB 3.0 类型 C 键入电缆。

- Windows 10 十月2020更新 (20H2) 或更高版本

## <a name="confirm-that-a-supported-usb-controller-is-available-on-the-target"></a>确认目标上提供了支持的 USB 控制器

在目标计算机上，启动设备管理器。

确认 *SYNOPSYS USB 3.0 Dual-Role 控制器* 已列出。

![显示 Synopsys USB 3.0 Dual-Role 控制器的 USB 节点的设备管理器在框中突出显示](images/kdnet-usb-eem-device-manager-target.png)

## <a name="determine-the-debugging-port-when-multiple-ports-are-available"></a>当有多个端口可用时确定调试端口

确定了支持调试的端口后，下一步是找到与该端口关联的物理 USB 连接器。

在 Surface Pro X 上，使用两个 USB C 端口中的下限用于 KDNET EEM 调试。

![Surface pro x 一侧的照片，其中显示了两个 usb c 端口 ](images/kdnet-usb-eem-surface-pro-x-usb-ports.png)

## <a name="use-kdnetexe-to-confirm-device-support-and-view-the-busparams-value"></a>使用 kdnet.exe 来确认设备支持并查看 busparams 值

若要指定将使用的调试端口，请使用 busparm。 通常只使用第一个 busparam，它是0或1，具体取决于设备。

ARM 设备使用 ACPI DBG2 表配置调试器，其中 busparams 指向 DBG2 表条目。 通常，设备不使用 busparams = 0，因为通常为串行设备 COM 保留 0 DBG2 表条目。

使用 kdnet.exe 实用工具显示支持 KDNET-EEM 传输调试的控制器的参数信息。

1. 确认主机系统上已安装 Windows 调试工具。 有关下载和安装调试器工具的信息，请参阅 [下载适用于 Windows 的调试工具](debugger-download-tools.md)。

2. 找到 kdnet.exe 和 VerifiedNICList.xml 文件。 默认情况下，它们位于此处。

   `C:\Program Files (x86)\Windows Kits\10\Debuggers\x64`

3. 在主计算机上，将这两个文件复制到网络共享或拇指驱动器，以便在目标计算机上可用。

4. 在目标计算机上创建 C:\KDNET 目录，并将 kdnet.exe 和 VerifiedNICList.xml 文件复制到该目录。

5. 在目标计算机上，以管理员身份打开“命令提示符”窗口。 输入此命令，验证目标计算机是否具有受支持的网络适配器并查看 busparams 值。

   ```console
   C:\KDNET>kdnet.exe

   Network debugging is not supported on any of the NICs in this machine.
   KDNET supports NICs from Intel, Broadcom, Realtek, Atheros, Emulex, Mellanox
   and Cisco.

   Network debugging is supported on the following USB controllers:
   busparams=1, Device-mode USB controller with Vendor ID: 5143 (Default)
   busparams=2, Device-mode USB controller with Vendor ID: 5143
   busparams=3, Device-mode USB controller with Vendor ID: 5143
   busparams=4, Device-mode USB controller with Vendor ID: 5143

   This Microsoft hypervisor supports using KDNET in guest VMs.
   ```

6. 由于 kdnet.exe 的输出指示支持的 USB 控制器的 busparams 值为1，因此我们可以继续。

## <a name="setting-up-the-target-computer"></a>设置目标计算机

按照以下步骤，使用 kdnet.exe 实用程序在目标电脑上配置调试器设置。

> [!IMPORTANT]
> 使用 bcdedit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 完成后，可以重新启用位保险箱并使用 BCDEdit 来更新启动信息。
> 在禁用安全功能时适当管理测试 PC。  

1. 使用如下所示的命令设置、busparams 值、主机系统的 IP 地址和端口并生成唯一的连接密钥。 169.254.255.255 IP 地址用于所有 USB EMM 连接。

2. 在建议的50000-50039 范围内，为你使用的每个目标/主机对选择唯一的端口地址。 示例中显示了50005。

```console

   C:\>kdnet.exe 169.254.255.255 50005

   Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
   Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

3. 将返回的密钥复制到 notepad.exe 文件中。 在显示的示例中，生成的键的值为：

   `2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p`

4. 使用 BCDEdit 命令检查参数是否与预期相同。 有关详细信息，请参阅 [BCDEdit/dbgsettings](../devtest/bcdedit--dbgsettings.md)

```console
   C:\>bcdedit /dbgsettings

   busparams               1
   key                     2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
   debugtype               NET
   hostip                  169.254.255.255
   port                    50005
   dhcp                    No
   The operation completed successfully.
 ```

## <a name="disable-the-firewall-on-the-host"></a>禁用主机上的防火墙

在主机上，禁用调试器的防火墙。

## <a name="connecting-windbg-to-the-target-for-kernel-debugging"></a>将 WinDbg 连接到用于内核调试的目标

在主计算机上，打开 WinDbg。 在 " **文件** " 菜单上，选择 " **内核调试**"。 在 "内核调试" 对话框中，打开 " **网络** " 选项卡。将之前保存的端口号和密钥粘贴到前面的 notepad.exe 文件中。 选择“确定”  。

你还可以通过打开命令提示符窗口并输入以下命令（其中是上面选择的端口）来启动 WinDbg 会话，它是上面 kdnet.exe 返回的键。 将上保存的项粘贴到前面的 notepad.exe 文件中。

   `windbg -k -d net:port=<YourDebugPort>,key=<YourKey>`

### <a name="reboot-the-target-computer"></a>重新启动目标计算机

连接调试器后，请重新启动目标计算机。 重新启动计算机的一种方法是在 `shutdown -r -t 0` 管理员的命令提示符下使用命令。

在目标计算机重新启动后，调试器应该会自动连接。

## <a name="troubleshooting-target"></a>目标故障排除

确认 windows 设备管理器中的 "网络适配器" 下是否存在 Windows KDNET-

设备属性显示了何时保留控制器供 Windows 内核调试器使用。

![显示 Synopsys USB 3.0 Dual-Role 控制器的 USB 节点的设备管理器，其中显示了控制器何时保留](images/kdnet-usb-eem-device-manager-properties-active-target.png)

## <a name="troubleshooting-host"></a>主机故障排除

确认 windows 设备管理器中的 "网络适配器" 下是否存在 Windows KDNET-

在主机上，将显示一个使用 USB 类型的 KDNET-EEM 连接。

![显示网络节点的 "设备管理器"，其中包含 Windows KDNET USB-EEM 网络适配器的节点](images/kdnet-usb-eem-device-manager-host-adapter.png)

## <a name="related-topics"></a>相关主题

[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)

[手动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection.md)

[手动设置通过 USB 3.0 线缆进行的内核模式调试](setting-up-a-usb-3-0-debug-cable-connection.md)

[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

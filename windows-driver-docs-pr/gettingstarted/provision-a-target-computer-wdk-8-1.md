---
title: 预配计算机以便进行驱动程序部署和测试 (WDK 10)
description: 预配目标计算机或测试计算机是配置计算机以自动部署、测试和调试驱动程序的过程。 若要预配计算机，请使用 Microsoft Visual Studio。
ms.assetid: A2615EE9-316E-4AE2-BBAA-B9E153090016
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8e496cedc09143109d499602003188e0cb4df20c
ms.sourcegitcommit: b1cdfbad7118bdeadff2e2003d59771b689c0553
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "82991954"
---
# <a name="provision-a-computer-for-driver-deployment-and-testing-wdk-10"></a>预配计算机以便进行驱动程序部署和测试 (WDK 10)

*预配目标计算机或测试计算机*是配置计算机以自动部署、测试和调试驱动程序的过程。 若要预配计算机，请使用 Microsoft Visual Studio。

一个测试和调试环境具有两台计算机：主计算机和目标计算机。 目标计算机也称为“测试计算机”。 在主计算机上的 Visual Studio 中开发和构建驱动程序。 调试程序在主计算机上运行，并在 Visual Studio 用户界面中可用。 测试和调试驱动程序时，驱动程序在目标计算机上运行。

主计算机和目标计算机必须能够彼此按名称 ping 通。 如果两台计算机已加入到同一工作组或同一网络域，则此操作可能更容易。 如果你的计算机位于工作组中，我们建议你使用路由器（而非集线器或交换机）连接计算机。

> [!TIP]
> 有关 WDK 和已知问题的最新信息，请查看 [WDK 支持论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=wdk)。

## <a name="prepare-the-target-computer-for-provisioning"></a>准备要预配的目标计算机

1. 在目标计算机上，安装将用于运行和测试驱动程序的操作系统。

2. [安装 WDK](../download-the-wdk.md)。 不过，你不需要安装 Visual Studio，除非你计划在目标计算机上进行驱动程序开发。

3. 如果在 x86 或 x64 目标计算机上启用了“安全启动”，请禁用该功能。 有关统一可扩展固件接口 (UEFI) 和安全启动的信息，请参阅 [UEFI 固件](https://go.microsoft.com/fwlink/p/?LinkID=309386)。

    如果目标计算机使用 ARM 处理器，则安装 Windows 调试策略。 该操作仅可以由 Microsoft 或目标计算机制造商完成。 无需禁用“安全启动”。

4. 在目标计算机上，运行与目标计算机平台匹配的 WDK 测试目标设置 MSI。 可以在 Remote 下的 Windows 驱动程序工具包 (WDK) 安装目录中找到该 MSI。

    例如：C:\\Program Files (x86)\\Windows Kits\\10\\Remote\\x64\\WDK Test Target Setup x64-x64\_en-us.msi

5. 如果目标计算机运行的是 N 或 KN 版本的 Windows，则安装适用于 N 和 KN 版本的 Windows 的媒体功能包：

    - [适用于 N 和 KN 版本的 Windows 8.1 的媒体功能包](https://go.microsoft.com/fwlink/p?linkid=329737)
    - [适用于 N 和 KN 版本的 Windows 8 的媒体功能包](https://go.microsoft.com/fwlink/p?linkid=329738)
    - [适用于 N 和 KN 版本的 Windows 7 的媒体功能包](https://go.microsoft.com/fwlink/p?linkid=329739)

6. 如果目标计算机运行的是 Windows Server，请查找刚才通过 WDK 测试目标设置 MSI 创建的 DriverTest 文件夹。 （示例：c:\\DriverTest）。 右键单击 **DriverTest** 文件夹，然后选择“属性”。 在“安全性”选项卡上，向“经过身份验证的用户”组授予“修改”权限。

验证主计算机和目标计算机是否可以彼此 ping 通。 打开命令提示符窗口，输入“**ping** ComputerName”。

如果主计算机和目标计算机已加入到一个工作组，但位于不同的子网上，则可能必须调整某些防火墙设置，以便主计算机和目标计算机可以通信。 请执行下列步骤：

1. 在目标计算机上的“控制面板”中，转到“网络和 Internet”&gt;“网络共享中心”。 请注意活动网络。 这将是**公用网络**、**专用网络**或**域**。
2. 在目标计算机上的“控制面板”中，转到“系统和安全”&gt;“Windows 防火墙”&gt;“高级设置”&gt;“入站规则”。
3. 在入站规则列表中，查找用于活动网络的所有网络发现规则。 （例如，查找具有**专用** **配置文件**的所有网络发现规则。）双击每个规则，并打开“作用域”选项卡。在“远程 IP 地址”下，选择“任何 IP 地址”。
4. 在入站规则列表中，查找用于活动网络的所有“文件和打印机共享”规则。 对于其中每个规则，双击该规则，并打开“作用域”选项卡。在“远程 IP 地址”下，选择“任何 IP 地址”。

## <a name="provision-the-target-computer"></a>预配目标计算机

现在，可以随时在 Visual Studio 中通过主计算机预配目标计算机。

1. 在主计算机上的 Visual Studio 中的“驱动程序”菜单上，选择“测试”&gt;“配置设备”。

    单击“添加新设备”。

2. 对于**网络主机名**，输入目标计算机的名称或本地 IP 地址。 选择“预配设备并选择调试程序设置”。

    ![“设备配置”对话框的屏幕截图](images/vs2015-device-configuration.png)

    单击 **下一步**。

3. 选择某种调试连接类型，并输入所需的参数。

    有关通过各种类型的连接设置调试的详细信息，请参阅 CHM 中的[手动设置内核模式调试](../debugger/setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)或 [Windows 调试工具](https://go.microsoft.com/fwlink/p/?linkid=223405)的联机文档。

4. 预配过程将需要几分钟时间，并且可能会自动重新启动目标计算机一到两次。 预配完成后，单击“完成”。

> [!TIP]
> 不支持通过 WDK 的自动预配过程来预配虚拟机。 但是，可以通过手动设置目标 VM 来测试 VM 上的驱动程序，如[分步回显实验室](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)中所述。

## <a name="see-also"></a>另请参阅

[将驱动程序部署到测试计算机](https://docs.microsoft.com/windows-hardware/drivers/develop/deploying-a-driver-to-a-test-computer)

---
title: 在 Visual Studio 中设置通过 USB 2.0 线缆进行的内核模式调试
description: 可以使用 Microsoft Visual Studio 设置和执行通过 USB 2.0 电缆内核模式调试。
ms.assetid: 3BEE43E2-32E5-4E7A-BA71-9ADB224578B1
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 30c1b5a2f6edf0973127742eb4f9d419a7a425ea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366365"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-20-cable-in-visual-studio"></a>在 Visual Studio 中设置通过 USB 2.0 线缆进行的内核模式调试

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

可以使用 Microsoft Visual Studio 设置和执行通过 USB 2.0 电缆内核模式调试。 若要使用内核模式调试的 Visual Studio，必须具有 Windows Driver Kit (WDK) 与 Visual Studio 集成。 有关如何安装集成的环境的信息，请参阅[Windows 驱动程序开发](https://go.microsoft.com/fwlink/p?linkid=301383)。

使用 Visual Studio 来设置调试的 USB 2.0 的替代方法，您还可以手动执行安装程序。 有关详细信息，请参阅[设置内核模式调试通过 USB 2.0 电缆手动](setting-up-a-usb-2-0-debug-cable-connection.md)。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。

通过 USB 2.0 连接调试需要以下硬件：

-   通用串行总线 (USB) 2.0 调试电缆。 此电缆不是标准的 USB 2.0 电缆，因为它具有一个额外的硬件组件，使其与 USB2 调试设备功能规范兼容。 可以通过执行"USB 2.0 调试电缆"的 Internet 搜索找到这些缆线。

-   在主计算机，EHCI (USB 2.0) 主控制器上

-   在目标计算机上，支持调试 EHCI (USB 2.0) 主控制器

## <a name="span-ididentifyingadebugportonthetargetcomputerspanspan-ididentifyingadebugportonthetargetcomputerspanspan-ididentifyingadebugportonthetargetcomputerspanidentifying-a-debug-port-on-the-target-computer"></a><span id="Identifying_a_Debug_Port_on_the_Target_Computer"></span><span id="identifying_a_debug_port_on_the_target_computer"></span><span id="IDENTIFYING_A_DEBUG_PORT_ON_THE_TARGET_COMPUTER"></span>标识目标计算机上的调试端口


1.  在目标计算机上启动 UsbView 工具。 UsbView 工具包含在为 Windows 调试工具。
2.  在 UsbView 中, 找到的所有主机控制器与 EHCI 规范兼容的。 例如，您可以查找列为增强的控制器。
3.  在 UsbView，依次展开 EHCI 主控制器的节点。 指示主机控制器支持调试，查找并查看调试端口号。 例如，UsbView 显示此支持调试端口 1 上 EHCI 主控制器的输出。

    ```console
    Xxx xxx xxx USB2 Enhanced Host Controller - 293A
    ...
    Debug Port Number:  1
    Bus.Device.Function (in decimal): 0.29.7
    ```

    **请注意**  许多 EHCI 主控制器支持 1，但某些 EHCI 主控制器支持调试端口 2 上的端口上进行调试。

     

4.  记下你想要用于调试的 EHCI 控制器的总线、 设备和函数编号。 UsbView 显示这些数字。 在前面的示例中，总线数为 0，设备号是 29，函数数为 7。

5.  确定 EHCI 控制器以及支持调试的端口号后下, 一步是找到正确的端口号与相关联的物理 USB 连接器。 若要查找实际的连接器，请将任何 USB 2.0 设备插入目标计算机上任何 USB 连接器。 刷新 UsbView 若要查看你的设备所在的位置。 如果 UsbView 显示你的设备连接到 EHCI 主控制器和标识为调试端口的端口，您已找到可用于调试的物理 USB 连接器。 它可能是没有外部的物理 USB 连接器与 EHCI 控制器上的调试端口相关联。 在这种情况下，您可以查找计算机内部的物理 USB 连接器。 执行相同的步骤来确定内部的 USB 连接器是否适用于内核调试。 如果找不到物理 USB 连接器 （外部或内部） 与该键相关联的调试端口，则不能将计算机用作目标通过 USB 2.0 电缆进行调试。

    **请注意**  请参阅[此批注](setting-up-a-usb-2-0-debug-cable-connection.md#what-if-usbview-shows-a-debug-capable-port)的异常。

     

## <a name="span-idconnectingtheusbdebugcablespanspan-idconnectingtheusbdebugcablespanspan-idconnectingtheusbdebugcablespanconnecting-the-usb-debug-cable"></a><span id="Connecting_the_USB_debug_cable"></span><span id="connecting_the_usb_debug_cable"></span><span id="CONNECTING_THE_USB_DEBUG_CABLE"></span>连接 USB 调试缆线


1.  验证主计算机未配置为作为目标的 USB 调试。 (如果有必要，请打开命令提示符窗口，以管理员身份，请输入**bcdedit /debug 关闭**，并重新启动。)
2.  在主计算机上使用 UsbView 查找 EHCI 主控制器和支持调试的端口。 如果可能，将 USB 2.0 调试电缆的一端插入不支持调试的 EHCI 端口到主机的计算机上）。 否则，将电缆插入任何 EHCI 端口在主计算机上。
3.  USB 2.0 调试电缆另一端插入之前标识目标计算机的连接器。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


1.  开始配置主机和目标计算机中所述[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。
2.  主机计算机上，在 Visual Studio 中，当您转至计算机配置对话框中，选择**预配计算机，并选择调试器设置**。
3.  有关**连接类型**，选择**USB**。

    ![屏幕截图显示调试程序的示例具有以下字段的值的设置： 连接类型、 目标名称和总线参数](images/setupusb2vs.png)

    有关**目标名称**，输入字符串来表示目标计算机。 此字符串不一定要在目标计算机; 的正式名称它可以是任何字符串，只要它满足这些限制创建：

    -   字符串的最大长度为 24 个字符。
    -   在字符串中的唯一字符是连字符 （-）、 下划线 (\_)，0 到 9 的数字和字母 A 到 Z （上限或下限的情况下）。

    如果目标计算机上有多个 USB 主控制器，请输入**总线参数**的值*b*。*d*。*f*，其中*b*， *d*，并且*f*是总线、 设备和你想要用于调试在 USB 主控制器的函数数量目标计算机。 总线、 设备和函数编号必须是以十进制格式 (示例：0.29.7).

4.  配置过程需要几分钟时间，并可能会自动重新启动目标计算机一次或两次。 该过程完成后，单击**完成**。

## <a name="span-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>验证目标计算机上的 dbgsettings


在目标计算机上，打开命令提示符窗口，以管理员身份，并输入以下命令：

**bcdedit /dbgsettings**

**bcdedit /enum**

```console
...
targetname              MyUsbTarget
debugtype               USB
debugport               1
baudrate                115200
...
busparams               0.29.7
...
```

确认*debugtype*是 USB 和*targetname*是在 Visual Studio 中指定主计算机的名称。 你可以忽略的值*debugport*并*baudrate*; 它们不适用于通过 USB 调试。

如果您输入**总线参数**在 Visual Studio 中，确认*busparams*您指定的总线参数匹配。

如果您看不到值为输入**总线参数**，输入以下命令：

**bcdedit /set "{dbgsettings}" busparams** <em>b</em> **.** <em>d</em> **.** <em>f</em>

其中*b*， *d*，并*f*是总线、 设备和已选择要用于调试的目标计算机上的 EHCI 控制器的函数数量。

例如：

**bcdedit /set "{dbgsettings}" busparams 0.29.7**

重新启动目标计算机。

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>启动调试会话的第一次


1.  USB 2.0 调试电缆连接到主机和目标计算机上进行调试您的 USB 2.0 端口。
2.  在主计算机上以管理员身份打开 Visual Studio。
3.  上**工具**菜单中，选择**附加到进程**。
4.  有关**传输**，选择**Windows 内核模式调试程序**。
5.  有关**限定符**，选择以前配置的目标计算机的名称。
6.  单击**附加**。

此时，主机计算机上安装的 USB 调试驱动程序。 这就是原因务必以管理员身份运行 Visual Studio。 安装 USB 调试驱动程序后，您不需要以管理员身份运行后续调试会话。

## <a name="span-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanspan-idstartingadebuggingsessionspanstarting-a-debugging-session"></a><span id="Starting_a_Debugging_Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>启动调试会话


1.  上，在 Visual Studio 中，主机计算机上**工具**菜单中，选择**附加到进程**。
2.  有关**传输**，选择**Windows 内核模式调试程序**。
3.  有关**限定符**，选择你在配置中输入的目标名称。
4.  单击**附加**。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 







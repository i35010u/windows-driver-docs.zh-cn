---
title: 在 Visual Studio 中设置通过 USB 2.0 线缆进行的内核模式调试
description: 你可以使用 Microsoft Visual Studio 通过 USB 2.0 电缆设置和执行内核模式调试。
ms.assetid: 3BEE43E2-32E5-4E7A-BA71-9ADB224578B1
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 214ecc93d865ed13aff379f5764135a3f600280a
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533910"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-20-cable-in-visual-studio"></a>在 Visual Studio 中设置通过 USB 2.0 线缆进行的内核模式调试

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

你可以使用 Microsoft Visual Studio 通过 USB 2.0 电缆设置和执行内核模式调试。 若要将 Visual Studio 用于内核模式调试，必须将 Windows 驱动程序工具包（WDK）与 Visual Studio 集成。 有关如何安装集成环境的信息，请参阅[使用 Visual Studio 进行调试](debugging-using-visual-studio.md)。

作为使用 Visual Studio 设置 USB 2.0 调试的替代方法，你可以手动执行设置。 有关详细信息，请参阅[通过 USB 2.0 电缆手动设置内核模式调试](setting-up-a-usb-2-0-debug-cable-connection.md)。

运行调试器的计算机称为 "*主机*"，正在调试的计算机称为 "*目标计算机*"。

通过 USB 2.0 连接进行调试需要以下硬件：

-   通用串行总线（USB）2.0 调试电缆。 此电缆不是标准 USB 2.0 电缆，因为它具有额外的硬件组件，使其与 USB2 调试设备功能规范兼容。 可以通过执行 "USB 2.0 调试电缆" 的 Internet 搜索来找到这些电缆。

-   在主计算机上，EHCI （USB 2.0）主机控制器

-   在目标计算机上，支持调试的 EHCI （USB 2.0）主机控制器

## <a name="span-ididentifying_a_debug_port_on_the_target_computerspanspan-ididentifying_a_debug_port_on_the_target_computerspanspan-ididentifying_a_debug_port_on_the_target_computerspanidentifying-a-debug-port-on-the-target-computer"></a><span id="Identifying_a_Debug_Port_on_the_Target_Computer"></span><span id="identifying_a_debug_port_on_the_target_computer"></span><span id="IDENTIFYING_A_DEBUG_PORT_ON_THE_TARGET_COMPUTER"></span>标识目标计算机上的调试端口


1.  在目标计算机上，启动 UsbView 工具。 UsbView 工具包含在 Windows 调试工具中。
2.  在 UsbView 中，找到与 EHCI 规范兼容的所有主机控制器。 例如，你可以查找列为 "增强" 的控制器。
3.  在 UsbView 中，展开 EHCI 主机控制器的节点。 查找主机控制器支持调试的指示，并查找调试端口的数量。 例如，UsbView 显示在端口1上支持调试的 EHCI 主机控制器的此输出。

    ```console
    Xxx xxx xxx USB2 Enhanced Host Controller - 293A
    ...
    Debug Port Number:  1
    Bus.Device.Function (in decimal): 0.29.7
    ```

    **注意**   许多 EHCI 主机控制器支持在端口1上进行调试，但某些 EHCI 主机控制器支持在端口2上进行调试。

     

4.  记下要用于调试的 EHCI 控制器的总线、设备和功能号。 UsbView 显示这些数字。 在前面的示例中，总线号为0，设备号为29，而函数号为7。

5.  确定 EHCI 控制器和支持调试的端口号后，下一步是找到与正确的端口号关联的物理 USB 连接器。 若要查找物理连接器，请将任何 USB 2.0 设备插入目标计算机上的任何 USB 连接器。 刷新 UsbView 以查看设备所在的位置。 如果 UsbView 显示已连接到 EHCI 主机控制器的设备和标识为调试端口的端口，则已找到可用于调试的物理 USB 连接器。 可能没有与 EHCI 控制器上的调试端口关联的外部物理 USB 连接器。 在这种情况下，可以在计算机中查找物理 USB 连接器。 执行相同的步骤，确定内部 USB 连接器是否适用于内核调试。 如果找不到与调试端口关联的物理 USB 连接器（外部或内部），则不能使用该计算机作为通过 USB 2.0 电缆进行调试的目标。

    **注意**   对于异常，请参阅[此注释](setting-up-a-usb-2-0-debug-cable-connection.md#what-if-usbview-shows-a-debug-capable-port)。

     

## <a name="span-idconnecting_the_usb_debug_cablespanspan-idconnecting_the_usb_debug_cablespanspan-idconnecting_the_usb_debug_cablespanconnecting-the-usb-debug-cable"></a><span id="Connecting_the_USB_debug_cable"></span><span id="connecting_the_usb_debug_cable"></span><span id="CONNECTING_THE_USB_DEBUG_CABLE"></span>连接 USB 调试电缆


1.  验证主机计算机未配置为 USB 调试的目标。 （如有必要，请以管理员身份打开命令提示符窗口，输入**bcdedit/debug off**，然后重新启动。）
2.  在主计算机上，使用 UsbView 查找 EHCI 主机控制器和支持调试的端口。 如果可能，请将 USB 2.0 调试电缆的一端插入不支持调试的 EHCI 端口（在主机计算机上）。 否则，请将电缆插入主机计算机上的任何 EHCI 端口。
3.  将 USB 2.0 调试电缆的另一端插入到之前在目标计算机上标识的连接器。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


1.  按照为[驱动程序部署和测试设置计算机（WDK 8.1）](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)中所述，开始配置主机和目标计算机。
2.  在主计算机上，在 Visual Studio 的 "计算机配置" 对话框中，选择 "**设置计算机"，然后选择 "调试器设置**"。
3.  对于 "**连接类型**"，请选择 " **USB**"。

    ![屏幕截图显示了具有以下字段的值的调试器设置示例：连接类型、目标名称和总线参数](images/setupusb2vs.png)

    对于 "**目标名称**"，请输入表示目标计算机的字符串。 此字符串不必是目标计算机的正式名称;它可以是您创建的任何字符串，只要它满足以下限制：

    -   字符串的最大长度为24个字符。
    -   字符串中的唯一字符是连字符（-）、下划线（ \_ ）、0到9的数字以及从 A 到 Z 的字母（大写或小写）。

    如果目标计算机上有多个 USB 主机控制器，请输入**总线参数**值*b*。*d.**f*，其中*b*、 *d*和*f*是要用于在目标计算机上进行调试的 USB 主机控制器的总线、设备和功能号。 总线、设备和函数编号必须采用 decimal 格式（例如：0.29.7）。

4.  配置过程需要几分钟的时间，并且可能会自动重启目标计算机一次或两次。 完成此过程后，单击 "**完成**"。

## <a name="span-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>验证目标计算机上的 dbgsettings


在目标计算机上，以管理员身份打开命令提示符窗口，然后输入以下命令：

**bcdedit/dbgsettings**

**bcdedit/enum**

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

验证*debugtype*是否为 USB， *targetname*是否是在主计算机上的 Visual Studio 中指定的名称。 可以忽略*debugport*和*波特率*的值;它们不适用于通过 USB 进行调试。

如果在 Visual Studio 中输入了**总线参数**，请验证*busparams*是否与指定的总线参数匹配。

如果看不到为**总线参数**输入的值，请输入以下命令：

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**.**<em>d.</em>**.**<em>f</em>

其中， *b*、 *d*和*f*是目标计算机上用于调试的 EHCI 控制器的总线、设备和功能号。

示例：

**bcdedit/set "{dbgsettings}" busparams 0.29。7**

重新启动目标计算机。

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>首次启动调试会话


1.  将 USB 2.0 调试电缆连接到在主机和目标计算机上选择进行调试的 USB 2.0 端口。
2.  在主计算机上，以管理员身份打开 Visual Studio。
3.  在 "**工具**" 菜单上，选择 "**附加到进程**"。
4.  对于 "**传输**"，请选择 " **Windows 内核模式调试程序**"。
5.  对于 "**限定符**"，选择以前配置的目标计算机的名称。
6.  单击 **“附加”** 。

此时，将在主计算机上安装 USB 调试驱动程序。 这就是以管理员身份运行 Visual Studio 非常重要的原因。 安装 USB 调试驱动程序之后，无需以管理员身份运行即可执行后续调试会话。

## <a name="span-idstarting_a_debugging_sessionspanspan-idstarting_a_debugging_sessionspanspan-idstarting_a_debugging_sessionspanstarting-a-debugging-session"></a><span id="Starting_a_Debugging_Session"></span><span id="starting_a_debugging_session"></span><span id="STARTING_A_DEBUGGING_SESSION"></span>启动调试会话


1.  在主计算机上，在 Visual Studio 的 "**工具**" 菜单中，选择 "**附加到进程**"。
2.  对于 "**传输**"，请选择 " **Windows 内核模式调试程序**"。
3.  对于 "**限定符**"，请选择在配置期间输入的目标名称。
4.  单击 **“附加”** 。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 







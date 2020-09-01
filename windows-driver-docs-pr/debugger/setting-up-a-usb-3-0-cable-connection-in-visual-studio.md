---
title: 在 Visual Studio 中设置通过 USB 3.0 线缆进行的内核模式调试
description: 你可以使用 Microsoft Visual Studio 通过 USB 3.0 电缆设置和执行内核模式调试。
ms.assetid: F8DD0475-13CE-464A-A491-AEFA962A96DB
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0402a0ded58820141bbbcd7134dd306fac29392b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212589"
---
# <a name="setting-up-kernel-mode-debugging-over-a-usb-30-cable-in-visual-studio"></a>在 Visual Studio 中设置通过 USB 3.0 线缆进行的内核模式调试

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

你可以使用 Microsoft Visual Studio 通过 USB 3.0 电缆设置和执行内核模式调试。 若要将 Visual Studio 用于内核模式调试，你必须将 Windows 驱动程序工具包 (WDK) 与 Visual Studio 集成。 有关如何安装集成环境的信息，请参阅 [使用 Visual Studio 进行调试](debugging-using-visual-studio.md)。

作为使用 Visual Studio 设置 USB 3.0 调试的替代方法，你可以手动执行设置。 有关详细信息，请参阅 [通过 USB 3.0 电缆手动设置内核模式调试](setting-up-a-usb-3-0-debug-cable-connection.md)。

运行调试器的计算机称为 " *主机*"，正在调试的计算机称为 " *目标计算机*"。

通过 USB 3.0 连接进行调试需要以下硬件：

-   USB 3.0 调试电缆。 这是一条 A 交叉电缆，只包含 USB 3.0 线路，无 Vbus。

-   在主计算机上，xHCI (USB 3.0) 主机控制器

-   在目标计算机上，支持调试的 xHCI (USB 3.0) 主机控制器

## <a name="span-idsetting_up_the_computer_usb3_manualspanspan-idsetting_up_the_computer_usb3_manualspanidentifying-a-debug-port-on-the-target-computer"></a><span id="setting_up_the_computer_usb3_manual"></span><span id="SETTING_UP_THE_COMPUTER_USB3_MANUAL"></span>标识目标计算机上的调试端口


1.  在目标计算机上，启动 UsbView 工具。 UsbView 工具包含在 Windows 调试工具中。
2.  在 UsbView 中，找到所有 xHCI 主机控制器。
3.  在 UsbView 中，展开 xHCI 主机控制器的节点。 查找主机控制器上的端口是否支持调试。

    ```console
    [Port1] 

    Is Port User Connectable:         yes
    Is Port Debug Capable:            yes
    Companion Port Number:            3
    Companion Hub Symbolic Link Name: USB#ROOT_HUB30#5&32bab638&0&0#{...}
    Protocols Supported:
     USB 1.1:                         no
     USB 2.0:                         no
     USB 3.0:                         yes
    ```

4.  记下要用于调试的 xHCI 控制器的总线、设备和功能号。 UsbView 显示这些数字。 在以下示例中，总线号为48，设备号为0，并且函数号为0。

    ```console
    USB xHCI Compliant Host Controller
    ...
    DriverKey: {36fc9e60-c465-11cf-8056-444553540000}\0020
    ...
    Bus.Device.Function (in decimal): 48.0.0
    ```

5.  确定了支持调试的 xHCI 控制器后，下一步是找到与 xHCI 控制器上的端口关联的物理 USB 连接器。 若要查找物理连接器，请将任何 USB 3.0 设备插入目标计算机上的任何 USB 连接器。 刷新 UsbView 以查看设备所在的位置。 如果 UsbView 显示已连接到 xHCI 主机控制器的设备，则已找到可用于 USB 3.0 调试的物理 USB 连接器。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


1.  按照为 [驱动程序部署设置计算机和测试 (WDK 8.1) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md)中所述，开始配置主机和目标计算机。
2.  在主计算机上，在 Visual Studio 的 "计算机配置" 对话框中，选择 " **设置计算机"，然后选择 "调试器设置**"。
3.  对于 " **连接类型**"，请选择 " **USB**"。

    ![屏幕截图显示了具有以下字段的值的调试器设置示例：连接类型、目标名称和总线参数](images/setupusbvs.png)

    对于 " **目标名称**"，请输入表示目标计算机的字符串。 此字符串不必是目标计算机的正式名称;它可以是您创建的任何字符串，只要它满足以下限制：

    -   字符串的最大长度为24个字符。
    -   字符串中的唯一字符是连字符 (-) 、下划线 (\_) 、数字0到9以及字母 A 到 Z (大写或小写。

    输入**总线参数**值*b*。*d.**f*，其中*b*、 *d*和*f*是要用于在目标计算机上进行调试的 USB 主机控制器的总线、设备和功能号。 总线、设备和函数编号必须采用 decimal 格式 (例如： 48.0.0) 。 这些值将显示在 "*常规*" 选项卡上的 "*位置*" 下设备管理器。  

4.  配置过程需要几分钟的时间，并且可能会自动重启目标计算机一次或两次。 完成此过程后，选择 " **完成**"。

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
busparams               48.0.0
```

验证 *debugtype* 是否为 USB， *targetname* 是否为主机应该上的 Visual Studio 中指定的名称。 可以忽略 *debugport* 和 *波特率*的值;它们不适用于通过 USB 进行调试。

验证 *busparams* 是否与指定的总线参数匹配。

如果看不到为 **总线参数**输入的值，请输入以下命令：

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**.**<em>d.</em>**.**<em>f</em>

其中， *b*、 *d*和 *f* 是目标计算机上选择用于调试的 xHCI 控制器的总线、设备和功能号。

示例：

**bcdedit/set "{dbgsettings}" busparams 48.0。0**

重新启动目标计算机。

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>首次启动调试会话


1.  将通用串行总线 (USB) 3.0 调试电缆连接到在主机和目标计算机上选择进行调试的 USB 3.0 端口。
2.  在主计算机上，以管理员身份打开 Visual Studio。
3.  在 " **工具** " 菜单上，选择 " **附加到进程**"。
4.  对于 " **传输**"，请选择 " **Windows 内核模式调试程序**"。
5.  对于 " **限定符**"，选择以前配置的目标计算机的名称。
6. 选择“附加”。

此时，将在主计算机上安装 USB 调试驱动程序。 这就是以管理员身份运行 Visual Studio 非常重要的原因。 安装 USB 调试驱动程序之后，无需以管理员身份运行即可执行后续调试会话。

## <a name="span-idstarting_the_debugging_session_usb3_vsspanspan-idstarting_the_debugging_session_usb3_vsspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session_usb3_vs"></span><span id="STARTING_THE_DEBUGGING_SESSION_USB3_VS"></span>启动调试会话


1.  在主计算机上，在 Visual Studio 的 " **工具** " 菜单中，选择 " **附加到进程**"。
2.  对于 " **传输**"，请选择 " **Windows 内核模式调试程序**"。
3.  对于 " **限定符**"，选择以前配置的目标计算机的名称。
4.  选择“附加”。

## <a name="span-idtroubleshooting_tips_for_debugging_over_usb_30spanspan-idtroubleshooting_tips_for_debugging_over_usb_30spantroubleshooting-tips-for-debugging-over-usb-30"></a><span id="troubleshooting_tips_for_debugging_over_usb_3.0"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_USB_3.0"></span>通过 USB 3.0 进行调试的疑难解答提示


在某些情况下，电源转换可能会干扰 USB 3.0 上的调试。 如果遇到此问题，请为 xHCI 主机控制器禁用选择性挂起 (及其用于调试的根中心) 。

1.  在设备管理器中，导航到 xHCI 主机控制器的节点。 选择并按住 (或右键单击 ") " 节点，然后选择 " **属性**"。 如果有 " **电源管理** " 选项卡，请打开该选项卡，并清除 " **允许计算机关闭此设备以节省电源** " 复选框。
2.  在设备管理器中，导航到 xHCI 主机控制器的根集线器的节点。 选择并按住 (或右键单击 ") " 节点，然后选择 " **属性**"。 如果有 " **电源管理** " 选项卡，请打开该选项卡，并清除 " **允许计算机关闭此设备以节省电源** " 复选框。

完成使用 xHCI 主机控制器进行调试时，为 xHCI 主机控制器启用选择性挂起。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

 


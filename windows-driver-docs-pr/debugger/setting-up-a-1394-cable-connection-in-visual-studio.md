---
title: 在 Visual Studio 中设置通过 1394 线缆进行的内核模式调试
description: 可以使用 Microsoft Visual Studio 设置和执行内核模式调试通过 1394年 (Firewire) 电缆。
ms.assetid: 07784500-83F1-4927-998F-7CEEEADAA2B0
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: fdba3fb40ce68c9fca9640221560a15b4239f4a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381952"
---
# <a name="setting-up-kernel-mode-debugging-over-a-1394-cable-in-visual-studio"></a>在 Visual Studio 中设置通过 1394 线缆进行的内核模式调试


> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

可以使用 Microsoft Visual Studio 设置和执行内核模式调试通过 1394年 (Firewire) 电缆。 若要使用内核模式调试的 Visual Studio，必须具有 Windows Driver Kit (WDK) 与 Visual Studio 集成。 有关如何安装集成的环境的信息，请参阅[Windows 驱动程序开发](https://go.microsoft.com/fwlink/p?linkid=301383)。

使用 Visual Studio 设置 1394年调试的替代方法，您还可以手动执行安装程序。 有关详细信息，请参阅[设置内核模式调试通过 1394年电缆手动](setting-up-a-1394-cable-connection.md)。

运行调试器的计算机称为*主机计算机*，和正在调试的计算机称为*目标计算机*。 在主机和目标计算机必须每个具有 1394年适配器。

## <a name="span-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanspan-idconfiguringthehostandtargetcomputersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


1.  连接到已选择在主机和目标计算机上进行调试的 1394 年控制器 1394年电缆。
2.  开始配置主机和目标计算机中所述[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)。
3.  主机计算机上，在 Visual Studio 中，转到计算机配置对话框后，选择**预配计算机，并选择调试器设置**。
4.  有关**连接类型**，选择**Firewire**。

    ![屏幕截图显示调试程序的示例具有以下字段的值的设置： 连接类型、 端口号、 密钥、 主机 ip 和总线参数](images/setup1394vs.png)

    有关**通道**，从 1 至第 62 输入所选的十进制数。

    **请注意**  不要设置通道为 0 时首次设置调试。 由于默认通道值为 0，软件假定存在不变，不会更新设置。 如果必须使用通道 0，第一次使用备用的通道 (1 至第 62)，然后切换到通道 0。

    如果有多个目标计算机上的 1394年控制器进入**总线参数**的值*b*。*d*。*f*，其中*b*， *d*，并且*f*是总线、 设备和想要使用在上进行调试的 1394年控制器函数数字目标计算机。 总线、 设备和函数编号必须是以十进制格式 (示例：4.4.0).

5.  配置过程需要几分钟时间，并可能会自动重新启动目标计算机一次或两次。 该过程完成后，单击**完成**。

## <a name="span-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanspan-idverifyingdbgsettingsonthetargetcomputerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>验证目标计算机上的 dbgsettings

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。

在目标计算机上，打开命令提示符窗口，以管理员身份，并输入以下命令：

**bcdedit /dbgsettings**

**bcdedit /enum**

```console
...
debugtype               1394
debugport               1
baudrate                115200
channel                 1
...
busparams               4.0.0
...
```

确认*debugtype*是 1394年和*通道*是你在 Visual Studio 中指定主计算机的通道数。 你可以忽略的值*debugport*并*baudrate*; 它们不适用于调试超过 1394年。

如果您输入**总线参数**在 Visual Studio 中，确认*busparams*您指定的总线参数匹配。

如果您看不到值为输入**总线参数**，输入以下命令：

**bcdedit /set "{dbgsettings}" busparams** <em>b</em>**.**<em>d</em>**.**<em>f</em>

其中*b*， *d*，并*f*是总线、 设备和已选择要用于调试的目标计算机上的 1394年控制器的函数数量。

例如：

**bcdedit /set "{dbgsettings}" busparams 4.4.0**

## <a name="span-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanspan-idstartingadebuggingsessionforthefirsttimespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>启动调试会话的第一次


1.  在主计算机上以管理员身份打开 Visual Studio。
2.  上**工具**菜单中，选择**附加到进程**。
3.  有关**传输**，选择**Windows 内核模式调试程序**。
4.  有关**限定符**，选择以前配置的目标计算机的名称。
5.  单击**附加**。

此时，主机计算机上安装的 1394年调试驱动程序。 这就是原因务必以管理员身份运行 Visual Studio。 1394 调试驱动程序安装后，您不需要以管理员身份运行后续调试会话。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  上，在 Visual Studio 中，主机计算机上**工具**菜单中，选择**附加到进程**。
2.  有关**传输**，选择**Windows 内核模式调试程序**。
3.  有关**限定符**，选择以前配置的目标计算机的名称。
4.  单击**附加**。

## <a name="span-idtroubleshootingtipsfordebuggingovera1394cablespanspan-idtroubleshootingtipsfordebuggingovera1394cablespantroubleshooting-tips-for-debugging-over-a-1394-cable"></a><span id="troubleshooting_tips_for_debugging_over_a_1394_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_1394_CABLE"></span>通过 1394年电缆进行调试的故障排除技巧


大多数 1394年调试问题引起的主机或目标计算机中使用多个的 1394 年控制器。 不支持在主计算机使用多个的 1394 年控制器。 1394 调试驱动程序，可以在主机上运行，只能与枚举注册表中的第一次 1394年控制器进行通信。 如果您有内置到主板和单独的 1394年卡的 1394年控制器，取出卡，或 （通过使用设备管理器） 禁用内置的控制器。

目标计算机可以具有多个的 1394 年控制器，尽管不建议这样做。 如果目标计算机具有母板上的 1394年控制器，以进行调试，如有可能使用该控制器。 如果没有附加 1394年卡片，应删除卡，并使用板载控制器。 另一种解决方案是计算机的禁用的 BIOS 设置中载入的 1394年控制器。

如果您决定有多个目标计算机上启用的 1394年控制器，必须指定总线参数，以便调试器知道哪一个控制器来声明以进行调试。 若要指定总线参数，打开设备管理器，并找到你想要用于调试的 1394年控制器。 打开控制器的属性页并记下的总线数、 设备数量和函数数量。 在提升的命令提示符窗口，输入以下命令，其中*b*， *d*，并*f*是十进制格式的总线、 设备和函数编号：

**bcdedit /set "{dbgsettings}" busparams** <em>b</em>**.**<em>d</em>**.**<em>f</em>

重新启动目标计算机。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

 

 







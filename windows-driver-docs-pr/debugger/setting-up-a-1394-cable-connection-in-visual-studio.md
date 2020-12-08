---
title: 在 Visual Studio 中设置通过 1394 线缆进行的内核模式调试
description: 可以使用 Microsoft Visual Studio 通过 1394 (火线) 电缆设置和执行内核模式调试。
ms.date: 04/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: a76c22bd3e03ec98120739c84dddbf88376d6e41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803627"
---
# <a name="setting-up-kernel-mode-debugging-over-a-1394-cable-in-visual-studio"></a>在 Visual Studio 中设置通过 1394 线缆进行的内核模式调试


> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

可以使用 Microsoft Visual Studio 通过 1394 (火线) 电缆设置和执行内核模式调试。 若要将 Visual Studio 用于内核模式调试，你必须将 Windows 驱动程序工具包 (WDK) 与 Visual Studio 集成。 有关如何安装集成环境的信息，请参阅 [使用 Visual Studio 进行调试](debugging-using-visual-studio.md)。

作为使用 Visual Studio 设置1394调试的替代方法，你可以手动执行设置。 有关详细信息，请参阅 [通过1394电缆手动设置 Kernel-Mode 调试](setting-up-a-1394-cable-connection.md)。

运行调试器的计算机称为 " *主机*"，正在调试的计算机称为 " *目标计算机*"。 主机和目标计算机必须都具有1394适配器。

## <a name="span-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanspan-idconfiguring_the_host_and_target_computersspanconfiguring-the-host-and-target-computers"></a><span id="Configuring_the_host_and_target_computers"></span><span id="configuring_the_host_and_target_computers"></span><span id="CONFIGURING_THE_HOST_AND_TARGET_COMPUTERS"></span>配置主机和目标计算机


1.  将1394电缆连接到在主机和目标计算机上选择进行调试的1394控制器。
2.  按照为 [驱动程序部署设置计算机和测试 (WDK 8.1) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md)中所述，开始配置主机和目标计算机。
3.  在主计算机上，在 Visual Studio 的 "计算机配置" 对话框中，选择 " **设置计算机" 并选择 "调试器设置**"。
4.  对于 " **连接类型**"，请选择 " **火线**"。

    ![屏幕截图显示了一个示例，其中包含以下字段的值：连接类型、端口号、密钥、主机 ip 和总线参数](images/setup1394vs.png)

    对于 " **通道**"，请输入从1到62的小数位数。

    **注意**  首次设置调试时，不要将通道设置为0。 由于默认通道值为0，因此软件会假定不存在更改，也不会更新设置。 如果必须使用通道0，请首先使用备用通道 (1 到 62) ，然后切换到通道0。

    输入 **总线参数** 值 *b*。*d.**f*，其中 *b*、 *d* 和 *f* 是要用于在目标计算机上进行调试的1394控制器的总线、设备和功能号。 总线、设备和函数编号必须采用 decimal 格式 (例如： 4.4.0) 。 这些值显示在“常规”选项卡上的“位置”下的设备管理器中 。  

5.  配置过程需要几分钟的时间，并且可能会自动重启目标计算机一次或两次。 完成此过程后，单击 " **完成**"。

## <a name="span-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanspan-idverifying_dbgsettings_on_the_target_computerspanverifying-dbgsettings-on-the-target-computer"></a><span id="Verifying_dbgsettings_on_the_Target_Computer"></span><span id="verifying_dbgsettings_on_the_target_computer"></span><span id="VERIFYING_DBGSETTINGS_ON_THE_TARGET_COMPUTER"></span>验证目标计算机上的 dbgsettings

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

在目标计算机上，以管理员身份打开命令提示符窗口，然后输入以下命令：

**bcdedit/dbgsettings**

**bcdedit/enum**

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

验证 " *debugtype* " 为1394，" *通道* " 是你在主计算机上的 Visual Studio 中指定的通道号。 可以忽略 *debugport* 和 *波特率* 的值;它们不适用于在1394上进行调试。

验证 *busparams* 是否与指定的总线参数匹配。

如果看不到为 **总线参数** 输入的值，请输入以下命令：

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**.**<em>d.</em>**.**<em>f</em>

其中， *b*、 *d* 和 *f* 是目标计算机上已选择用于调试的1394控制器的总线、设备和功能号。

例如：

**bcdedit/set "{dbgsettings}" busparams 4.4。0**

## <a name="span-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanspan-idstarting_a_debugging_session_for_the_first_timespanstarting-a-debugging-session-for-the-first-time"></a><span id="Starting_a_Debugging_Session_for_the_First_Time"></span><span id="starting_a_debugging_session_for_the_first_time"></span><span id="STARTING_A_DEBUGGING_SESSION_FOR_THE_FIRST_TIME"></span>首次启动调试会话


1.  在主计算机上，以管理员身份打开 Visual Studio。
2.  在 " **工具** " 菜单上，选择 " **附加到进程**"。
3.  对于 " **传输**"，请选择 " **Windows 内核模式调试程序**"。
4.  对于 " **限定符**"，选择以前配置的目标计算机的名称。
5.  单击 **“附加”** 。

此时，将在主计算机上安装1394调试驱动程序。 这就是以管理员身份运行 Visual Studio 非常重要的原因。 安装了1394调试驱动程序之后，无需以管理员身份运行即可执行后续调试会话。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-a-debugging-session"></a><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>启动调试会话


1.  在主计算机上，在 Visual Studio 的 " **工具** " 菜单中，选择 " **附加到进程**"。
2.  对于 " **传输**"，请选择 " **Windows 内核模式调试程序**"。
3.  对于 " **限定符**"，选择以前配置的目标计算机的名称。
4.  单击 **“附加”** 。

## <a name="span-idtroubleshooting_tips_for_debugging_over_a_1394_cablespanspan-idtroubleshooting_tips_for_debugging_over_a_1394_cablespantroubleshooting-tips-for-debugging-over-a-1394-cable"></a><span id="troubleshooting_tips_for_debugging_over_a_1394_cable"></span><span id="TROUBLESHOOTING_TIPS_FOR_DEBUGGING_OVER_A_1394_CABLE"></span>通过1394电缆进行调试的故障排除提示


大多数1394调试问题都是在主机或目标计算机中使用多个1394控制器导致的。 不支持在主机计算机中使用多个1394控制器。 在主机上运行的1394调试驱动程序只能与注册表中枚举的第一个1394控制器进行通信。 如果主板内置了1394控制器和一个单独的1394卡，请删除卡，或使用内置控制器) 设备管理器来禁用 (。

目标计算机可以有多个1394控制器，尽管不建议这样做。 如果目标计算机在主板上有1394控制器，请尽可能使用该控制器进行调试。 如果有其他1394卡，则应拔下卡并使用板载控制器。 另一种解决方案是在计算机的 BIOS 设置中禁用板载1394控制器。

如果你决定在目标计算机上启用多个1394控制器，则必须指定总线参数，以便调试器知道要对哪个控制器进行调试。 若要指定总线参数，请打开设备管理器，然后找到要用于调试的1394控制器。 打开控制器的 "属性" 页，记下 "总线号码"、"设备编号" 和 "功能编号"。 在提升的命令提示符窗口中，输入以下命令，其中 *b*、 *d* 和 *f* 是以十进制格式表示的总线、设备和函数编号：

**bcdedit/set "{dbgsettings}" busparams** <em>b</em>**.**<em>d.</em>**.**<em>f</em>

重新启动目标计算机。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在 Visual Studio 中设置内核模式调试](setting-up-kernel-mode-debugging-in-visual-studio.md)

 


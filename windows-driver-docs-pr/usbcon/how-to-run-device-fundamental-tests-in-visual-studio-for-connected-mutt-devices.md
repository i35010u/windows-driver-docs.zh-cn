---
Description: 介绍适用于连接到可用端口的 MUTT 设备必须运行设备基础测试。
title: 在 Visual Studio 中运行系统电源说明测试 MUTT 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61c9c14b4dbea00de855e89135593836ba81f385
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366053"
---
# <a name="how-to-run-system-power-devfund-tests-in-visual-studio-for-mutt-devices"></a>如何在 Visual Studio 中针对 MUTT 设备运行系统电源 devfund 测试


介绍适用于连接到可用端口，MUTT 设备必须运行设备基础测试来执行压力和传输的测试和系统电源测试。

这些测试它们执行系统电源事件的同时执行简单的设备传输。 请注意，说明测试只能在 Windows 8 上运行。 您不能[运行压力和传输测试](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)并同时测试系统电源。 在单独的系统上执行这些测试。 但是，压力传输与系统之间切换电源测试。 为此，请完成第一组测试，重新启动计算机，然后按照下一个测试的说明进行操作。

## <a name="how-to-run-device-fundamental-devfund-tests-in-visual-studio-for-connected-mutt-devices"></a>如何运行设备基础 （说明） 测试在 Visual Studio 中连接的 MUTT 设备


说明测试是一系列用于测试的驱动程序和硬件的测试。 与 Windows 8 的 WDK 中包含这些测试。 可以运行的 WDK 外接程序到 Microsoft Visual Studio Professional 2012 RC，并从你的开发环境中运行这些测试。

### <a name="prerequisites"></a>先决条件

在开始运行说明测试之前，请确保满足以下要求：

-   若要运行这些测试，你将需要至少两台计算机： 主机和测试。 配置主机和测试用于测试和调试的计算机。

    -   必须为 Windows 8 中安装 Microsoft Visual Studio Professional 2012 和 Windows Driver Kit (WDK)。
    -   测试计算机必须运行 Windows 8 的最新版本。

    你可以下载 Visual Studio 和从 WDK[下载的 Windows 硬件开发](https://go.microsoft.com/fwlink/p/?linkid=309780)。

    有关配置的说明，请参阅[配置一台计算机的驱动程序部署、 测试和调试](https://go.microsoft.com/fwlink/p/?linkid=235504)。

-   主机计算机连接到测试计算机之前，你必须在测试计算机上启用文件和打印共享以及网络发现。 您可以启用这些选项在控制面板中或通过在提升的命令提示符中使用以下命令：

    `netsh.exe advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes`

-   设置和配置 MUTT 设备并安装固件。 有关详细信息，请参阅[如何进行准备，测试系统](mutt-testing-options.md)。
-   设置测试计算机。 有关说明，请参阅[配置一台计算机的驱动程序部署、 测试和调试](https://go.microsoft.com/fwlink/p/?linkid=235504)。

### <a name="scheduling-tests"></a>计划测试

1.  选择要在测试计算机上运行的测试。 有关说明，请参阅**步骤 2:选择要在测试计算机上运行的测试**中[如何测试在运行时使用 Visual Studio 的驱动程序](https://go.microsoft.com/fwlink/p/?linkid=290770)。
2.  在下图中所示设置以下运行时参数。

    -   DQ:类 = USBTest
    -   TestCycles:100

    ![visual studio 测试组](images/fig11-vs-testgroup.png)

3.  配置测试参数。 有关配置信息，请参阅**步骤 3:配置测试参数**中[如何测试在运行时使用 Visual Studio 的驱动程序](https://go.microsoft.com/fwlink/p/?linkid=290770)。
4.  运行测试。 要运行的测试有关的信息，请参阅**步骤 5:在测试计算机上运行测试**中[如何测试在运行时使用 Visual Studio 的驱动程序](https://go.microsoft.com/fwlink/p/?linkid=290770)。

### <a name="recommended-tests-to-schedule-with-the-connected-mutt-device"></a>推荐的测试计划与连接的 MUTT 设备

-   与 IO 进入睡眠状态之前和之后
-   进入睡眠状态与 IO 期间 (Basic)
-   IO 前后的 PNP （禁用和启用）

有关上述列表中测试的详细信息，请参阅**有关设备基本测试**中[如何选择和配置设备基础测试](https://go.microsoft.com/fwlink/p/?linkid=316387)。

## <a name="related-topics"></a>相关主题
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  




---
description: 介绍必须为附加到可用端口的 MUTT 设备运行的设备基础测试。
title: 在 Visual Studio for MUTT 设备中运行系统电源 devfund 测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81ee5a66337d203baaa0aca39487f567c97bb576
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969138"
---
# <a name="how-to-run-system-power-devfund-tests-in-visual-studio-for-mutt-devices"></a>如何在 Visual Studio 中针对 MUTT 设备运行系统电源 devfund 测试


介绍必须为附加到可用端口的 MUTT 设备运行的设备基本测试，以执行压力和传输测试以及系统电源测试。

这些测试将在执行系统电源事件的同时执行简单的设备传输。 请注意，只能在 Windows 8 上运行 devfund 测试。 不能同时 [运行压力测试和传输测试](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md) 以及系统电源测试。 在单独的系统上执行这些测试。 但是，可以在压力传输和系统电源测试之间切换。 为此，请完成第一组测试，重新启动计算机，然后按照下一次测试的说明进行操作。

## <a name="how-to-run-device-fundamental-devfund-tests-in-visual-studio-for-connected-mutt-devices"></a>如何在 Visual Studio 中运行设备基础 (devfund) 用于连接的 MUTT 设备的测试


Devfund 测试是用于测试驱动程序和硬件的测试集合。 这些测试与适用于 Windows 8 的 WDK 一起提供。 可以运行 WDK 外接程序来 Microsoft Visual Studio Professional 2012 RC，并从开发环境运行这些测试。

### <a name="prerequisites"></a>先决条件

在开始运行 devfund 测试之前，请确保满足以下要求：

-   若要运行这些测试，你至少需要两台计算机：主机和测试。 配置主机和测试计算机，以便进行测试和调试。

    -   你必须在 Windows 8 (WDK) 安装 Microsoft Visual Studio Professional 2012 和 Windows 驱动程序工具包。
    -   测试计算机必须运行 Windows 8 的最新版本。

    你可以从 [下载下载适用于 Windows 硬件开发的](https://go.microsoft.com/fwlink/p/?linkid=309780)Visual STUDIO 和 WDK。

    有关配置的说明，请参阅 [配置计算机以进行驱动程序部署、测试和调试](https://go.microsoft.com/fwlink/p/?linkid=235504)。

-   在将主机连接到测试计算机之前，必须在测试计算机上启用文件和打印共享和网络发现。 可以在 "控制面板" 中启用这些选项，也可以通过在提升的命令提示符中使用以下命令来启用：

    `netsh.exe advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes`

-   设置并配置 MUTT 设备并安装固件。 有关详细信息，请参阅 [如何准备测试系统](mutt-testing-options.md)。
-   设置测试计算机。 有关说明，请参阅 [配置计算机以进行驱动程序部署、测试和调试](https://go.microsoft.com/fwlink/p/?linkid=235504)。

### <a name="scheduling-tests"></a>计划测试

1.  选择要在测试计算机上运行的测试。 有关说明，请参阅步骤2：[使用 Visual Studio 在运行时中的如何测试驱动程序](https://go.microsoft.com/fwlink/p/?linkid=290770)中的 "**选择要在测试计算机上运行的测试**"。
2.  按下图所示设置以下运行时参数。

    -   DQ：类 = "USBTest"
    -   TestCycles：100

    ![visual studio 测试组](images/fig11-vs-testgroup.png)

3.  配置测试参数。 有关配置的详细信息，请参阅步骤3：[使用 Visual Studio 在运行时测试驱动程序](https://go.microsoft.com/fwlink/p/?linkid=290770)中的 "**配置测试参数**"。
4.  运行测试。 有关要运行的测试的信息，请参阅 "[如何使用 Visual Studio 在运行时测试驱动程序](https://go.microsoft.com/fwlink/p/?linkid=290770)" 中的**步骤5：在测试计算机上运行测试**。

### <a name="recommended-tests-to-schedule-with-the-connected-mutt-device"></a>建议用于使用连接的 MUTT 设备进行计划的测试

-   在 IO 前后睡眠
-    (基本) 期间休眠 IO
-   PNP (在之前和之后使用 IO 禁用和启用 ) 

有关上述列表中的测试的详细信息，请参阅关于[如何选择和配置设备基本测试](https://go.microsoft.com/fwlink/p/?linkid=316387)中**的关于设备基础测试**。

## <a name="related-topics"></a>相关主题
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  




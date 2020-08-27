---
description: 使用 MUTT 设备之前，必须准备测试系统。
title: 如何准备测试系统以运行 MUTT 测试工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c61a44b4645ae1f16fc08b6e08811d92295ffbb8
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969326"
---
# <a name="how-to-prepare-the-test-system-to-run-mutt-test-tools"></a>如何准备测试系统以运行 MUTT 测试工具


使用 MUTT 设备之前，必须准备测试系统。

## <a name="prerequisites"></a>先决条件


本文档中的说明基于以下假设：

-   你已了解 Windows 命令行界面。 安装测试工具需要提升的命令窗口。 对于该窗口，您可以使用 "以 **管理员身份运行** " 选项打开命令提示符窗口。
-   你熟悉 Windows 驱动程序工具包附带的工具 (WDK) 。
-   你熟悉内核调试工具。

**注意**   此设置适用于 MUTT、MUTTPack、SuperMUTT 和 SuperMUTT Pack。 有关这些设备的详细信息，请参阅 [MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。

 

## <a name="instructions"></a>Instructions


**准备系统以运行用于 USB 硬件测试的 MUTT 测试工具**

1.  将测试系统连接到内核调试器。

    有关详细信息，请参阅 [下载并安装适用于 windows](https://go.microsoft.com/fwlink/p/?linkid=236405) 和 [Windows 调试](https://go.microsoft.com/fwlink/p/?linkid=242503)的调试工具。

2.  将 MUTT 设备连接到主机控制器或集线器的每个可用端口进行测试。

    在运行由 MUTT 软件包安装的安装脚本之前，必须将 MUTT 设备连接到测试系统。

    有关推荐的测试配置的信息，请参阅本文档中的 MUTT 拓扑。

3.  在测试系统上打开提升的命令窗口，并导航到复制了测试工具的文件夹。
4.  在提升的命令窗口中，安装必需的 MUTT driver **C： \\ usbTest \\ pnputil – usbfx2**

    如果要使用驱动程序验证程序进行测试，则可以运行 **install** ，而不是上一个命令。 这将安装所需的驱动程序并配置驱动程序验证程序。 请注意，使用 **install .cmd** 是可选的。

5.  安装测试驱动程序时，将出现以下对话框：

    !["windows 安全" 对话框](images/fig9-winsec.png)

    选中 **"始终信任来自 ' Microsoft Corporation ' 的软件"** 以防止在运行测试时显示该对话框。

    **安装**完成后，测试系统计算机将重新启动。

6.  将 MUTT 切换到新的驱动程序 **C： \\ usbTest \\ MuttUtil – UpdateDriver usbfx2**
7.  将 MUTT 更新为最新的固件 **C： \\ usbTest \\MuttUtil.exe-UpdateFirmware**
8.  如果你的测试系统正在运行 Windows 8，则建议你在开始测试之前对主机控制器执行快速验证。

    在提升的命令提示符窗口中运行以下命令，以收集有关连接到系统： **C： \\ usbTest \\ xhciwmi**的主机控制器和集线器的信息。

    该工具在命令窗口中显示有关主机控制器的信息。 信息包括供应商 ID、设备 ID、修订版 ID 和固件版本。 如果测试中的主机控制器存在已知问题，请考虑更新固件。

### <a name="tracing-and-logging-events-in-the-usb-driver-stack"></a>USB 驱动程序堆栈中的跟踪和日志记录事件

请参阅 https://aka.ms/usbtrace 获取说明，并下载用于从 USB 驱动程序捕获 ETW 跟踪的脚本。

## <a name="related-topics"></a>相关主题
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  




---
Description: Before using MUTT devices, you must prepare the test system.
title: 如何准备测试系统以运行 MUTT 测试工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e7c60595a621275c95fa98fc9d448e0a2f5e116
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575890"
---
# <a name="how-to-prepare-the-test-system-to-run-mutt-test-tools"></a>如何准备测试系统以运行 MUTT 测试工具


在使用之前 MUTT 设备，必须准备的测试系统。

## <a name="prerequisites"></a>先决条件


本文档中的说明基于以下假设：

-   你已了解的 Windows 命令行界面。 测试工具的安装需要提升的命令窗口。 为该窗口中，您可以打开命令提示符窗口使用**以管理员身份运行**选项。
-   您熟悉使用 Windows Driver Kit (WDK) 中包含的工具。
-   您熟悉的内核调试工具。

**请注意**  此安装程序应用到 MUTT、 MUTTPack、 SuperMUTT 和 SuperMUTT 包。 有关这些设备的详细信息，请参阅[MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。

 

## <a name="instructions"></a>说明


**若要准备系统以运行 MUTT USB 硬件测试的测试工具**

1.  连接到内核调试程序的测试系统。

    有关详细信息，请参阅[下载和为 Windows 中安装调试的工具](https://go.microsoft.com/fwlink/p/?linkid=236405)并[Windows 调试](https://go.microsoft.com/fwlink/p/?linkid=242503)。

2.  将 MUTT 设备附加到的主机控制器或中心，以测试每个可用端口。

    在运行安装 MUTT 软件包的安装脚本之前，必须将 MUTT 设备附加到测试系统。

    有关建议的测试配置的信息，请参阅本文档中的 MUTT 拓扑。

3.  打开测试系统上的提升的命令窗口并导航到在其中复制测试工具的文件夹。
4.  在提升的命令窗口中，安装必要的 MUTT 驱动程序**c:\\usbTest\\pnputil – i – a usbfx2.inf**

    如果你想要测试使用驱动程序验证程序，则可以运行**install.cmd**而不是上一命令。 这将安装必需的驱动程序以及配置驱动程序验证程序。 请注意，使用**install.cmd**是可选的。

5.  安装测试驱动程序时显示以下对话框：

    ![windows 安全对话框](images/fig9-winsec.png)

    检查**始终信任来自"Microsoft Corporation"的软件**可阻止对话框出现时在运行测试。

    测试系统计算机将重新启动后**install.cmd**已完成安装。

6.  切换到新的驱动程序的 MUTT **c:\\usbTest\\MuttUtil – UpdateDriver usbfx2.inf**
7.  使用最新的固件更新 MUTT **c:\\usbTest\\MuttUtil.exe UpdateFirmware**
8.  如果您的测试系统正在运行 Windows 8，我们建议在开始测试之前执行快速验证您的主控制器。

    从提升的命令提示符窗口，运行以下命令，以收集有关你的主控制器和连接到系统的中心的信息：**C:\\usbTest\\xhciwmi-验证**。

    该工具在命令窗口中显示有关主机控制器的信息。 信息包括供应商 ID、 设备 ID、 修订 ID 和固件版本。 如果已知待测试的主机控制器存在问题，请考虑更新固件。

### <a name="tracing-and-logging-events-in-the-usb-driver-stack"></a>跟踪和日志事件记录在 USB 驱动程序堆栈

转到 https://aka.ms/usbtrace有关说明和下载用于捕获从 USB 驱动程序的 ETW 跟踪的脚本。

## <a name="related-topics"></a>相关主题
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  




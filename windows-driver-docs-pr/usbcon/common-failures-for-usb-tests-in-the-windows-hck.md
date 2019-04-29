---
Description: USB 中的测试 Windows HLK 的常见故障。
title: USB 测试 Windows HLK 中常见的故障
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b8ff4b0debb546befba3ca04ff21268c346b213
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392099"
---
# <a name="common-failures-for-usb-tests-in-the-windows-hlk"></a>USB 测试 Windows HLK 中常见的故障


USB 中的测试 Windows HLK 的常见故障。

## <a name="devfund-tests-for-usb"></a>有关 USB 的说明测试


-   错误条件：设备状态检查失败，并出现错误，指示 MUTT 设备不存在。

    1.  SuperMUTT 运行 Winusb.sys 或 Usbtcd.sys 作为驱动程序。 你可以获取该驱动程序和驱动程序安装包文件通过安装[MUTT 软件包](https://msdn.microsoft.com/windows/hardware/jj590752)。 有关详细信息，请参阅[MUTT 软件包中的工具](mutt-software-package.md)。
    2.  请确保设备管理器中显示为该 SuperMUTT 的硬件 ID"USB\\VID\_045E & PID\_078F"。 **请注意**  PID\_078E 不正确。
    3.  请确保该设备管理器 (**视图&gt;依连接排序设备**) 显示了枚举该 SuperMUTT xHCI 控制器的下一级。
    4.  在 USBView，请确保在 SuperSpeed SuperMUTT 设备操作。 **请注意**  你可以安装从 USBView**的 Windows 中安装调试的工具包**中 Microsoft Windows 软件开发工具包 (SDK)。 或者，在调试程序文件夹中 Windows Driver Kit (WDK) 中安装 USBView。
    5.  请确保 MUTT 固件是最新。 从提升的提示符运行"muttutil updatefirmware"目录中的安装位置[MUTT 软件包](https://msdn.microsoft.com/windows/hardware/jj590752)。

    如果问题仍然存在，则报告这些附件的问题：
    -   设备管理器屏幕截图和 USBView 显示项 1-4 上述列表中。
    -   输出[MuttUtil](muttutil.md)命令。
-   错误条件：说明在简单的 I/O 传输过程中失败。
    1.  转到 https://aka.ms/usbtrace并下载 usbtrace.cmd。
    2.  使用此脚本可以捕获驱动程序日志，以便进一步进行调查的事件。
    3.  附加的 %systemdrive%的所有内容\\Windows\Tracing 与 bug。
    4.  保存并附加失败测试的.hlkx 文件。
-   错误条件：MUTT 设备连接到系统，但未安装正确的驱动程序。

    最可能的驱动程序安装失败或设备不具有最新的固件。 安装 Winusb.sys 或 Usbtcd.sys 作为驱动程序。 你可以获取该驱动程序和驱动程序安装包文件通过安装[MUTT 软件包](https://msdn.microsoft.com/windows/hardware/jj590752)。

 

 





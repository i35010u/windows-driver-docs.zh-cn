---
description: Windows HLK 中的 USB 测试常见故障。
title: Windows HLK 中的 USB 测试常见故障
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca2b011a68427471686df6eefc382dccda4533b1
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968992"
---
# <a name="common-failures-for-usb-tests-in-the-windows-hlk"></a>Windows HLK 中的 USB 测试常见故障


Windows HLK 中的 USB 测试常见故障。

## <a name="devfund-tests-for-usb"></a>USB 的 DevFund 测试


-   错误情况：设备状态检查失败，并显示一条错误消息，指出 MUTT 设备不存在。

    1.  SuperMUTT 作为驱动程序运行 Winusb.sys 或 Usbtcd.sys。 可以通过安装 [MUTT](https://msdn.microsoft.com/windows/hardware/jj590752)软件包获取驱动程序和驱动程序安装包文件。 有关详细信息，请参阅 [MUTT 软件包中的工具](mutt-software-package.md)。
    2.  请确保设备管理器将 SuperMUTT 的硬件 ID 显示为 "USB \\ VID \_ 045E&PID \_ 078F"。 **注意**   PID \_ 078E 不正确。
    3.  请确保设备管理器 (** &gt; 按连接查看设备** ") 显示 XHCI 控制器的 SuperMUTT 枚举下游。
    4.  在 USBView 中，确保 SuperMUTT 设备在 SuperSpeed 上运行。 **注意**   你可以从 Microsoft Windows 软件开发工具包 (SDK) 中的 "**安装适用于 Windows 的调试工具" 包**中安装 USBView。 或者，USBView 安装在 Windows 驱动程序工具包 (WDK) 的 "调试器" 文件夹中。
    5.  请确保 MUTT 固件是最新版本。 在提升的提示符下，在安装 [MUTT 软件包](https://msdn.microsoft.com/windows/hardware/jj590752)的目录中运行 "muttutil-updatefirmware"。

    如果问题仍然存在，请报告以下附件的问题：
    -   显示前面列表中的项目1-4 的设备管理器和 USBView 的屏幕截图。
    -   [MuttUtil](muttutil.md)命令的输出。
-   错误情况： DevFund 在简单的 i/o 传输过程中失败。
    1.  中转到 https://aka.ms/usbtrace 并下载 usbtrace。
    2.  使用此脚本捕获事件的驱动程序日志以便进一步调查。
    3.  将% SystemDrive% Windows\Tracing 的所有内容附加 \\ 到您的 bug 中。
    4.  为失败的测试保存并附加 hlkx 文件。
-   错误情况： MUTT 设备已连接到系统，但未安装正确的驱动程序。

    最可能的驱动程序安装失败或设备没有最新的固件。 将 Winusb.sys 或 Usbtcd.sys 安装为驱动程序。 可以通过安装 [MUTT](https://msdn.microsoft.com/windows/hardware/jj590752)软件包获取驱动程序和驱动程序安装包文件。

 

 





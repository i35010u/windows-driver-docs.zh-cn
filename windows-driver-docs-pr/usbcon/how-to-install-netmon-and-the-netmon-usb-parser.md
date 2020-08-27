---
description: 本主题提供有关 Netmon 和 USB ETW 分析器的安装信息。
title: 如何安装 Netmon 和 USB ETW 分析程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6664a6300d9cc1fb0a11ccfee786c545471f2949
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968980"
---
# <a name="how-to-install-netmon-and-usb-etw-parsers"></a>如何安装 Netmon 和 USB ETW 分析程序

本主题提供有关 Netmon 和 USB ETW 分析器的安装信息。

从 Microsoft 下载中心安装 Netmon，然后从 [Windows 驱动程序工具包 (WDK) ](https://msdn.microsoft.com/windows/hardware/hh852362.aspx)安装 USB ETW 分析器。 Netmon 版本3.3 及更高版本支持 USB ETW 分析。

## <a name="to-install-the-netmon-tool-and-the-netmon-usb-parser"></a>安装 Netmon 工具和 Netmon USB 分析器

1. 确定计算机是否正在运行32位 Windows 或64位 Windows：

    1. 打开 " **开始** " 菜单，右键单击 " **计算机** " 和 "查看 **属性**"。
    2. 查看 " **系统类型** " 字段。

    如果你的系统类型为32位操作系统，你将使用 x86 下载。 如果你的系统类型为64位操作系统，而你的处理器为 Itanium，你将使用 ia64 下载。 对于其他处理器类型，请使用 x64 或 AMD64 下载。

2. 安装 Netmon：
    1. 在 Microsoft 下载中心的 " [Windows 网络监视器](https://go.microsoft.com/fwlink/p/?linkid=103158) " 页上，阅读该工具的说明。
    2. 在页面底部的 " **此下载中的文件** " 下，单击系统类型的 " **下载** " 按钮。
    3. 下载并运行 .exe 文件以启动安装向导。
    4. 当要求你选择安装类型时，请选择 " **典型** "。

3. 从 [Windows 驱动程序工具包 8](https://msdn.microsoft.com/windows/hardware/hh852362.aspx)安装 WDK。
4. 允许执行 PowerShell 脚本：
    1. 在 "开始" 屏幕上，键入 "powershell"，右键单击 Windows PowerShell 结果，然后选择 "以 **管理员身份运行**"。
    2. 在 PowerShell 窗口中，键入以下命令：

        ```syntax
        Set-ExecutionPolicy RemoteSigned -Force
        ```

    3. 关闭 PowerShell 窗口。
    4. 打开 PowerShell 窗口， (不需要以 **管理员身份运行**) 并运行以下命令。 如果已将工具包安装到其他位置，请调整该路径：

        ```syntax
        cd "C:\Program Files (x86)\Windows Kits\8.0\Tools\x86\Network Monitor Parsers\usb"
        ..\NplAutoProfile.ps1
        ```

    5. 重新启动 Netmon 以应用所做的更改。

5. 验证配置文件在 Netmon 中是否处于活动状态。
    1. 在“工具”菜单上，选择“选项”。
    2. 在 " **分析器配置文件** " 选项卡上，确保 **AutoProfile 生成的) ** 设置为活动 (。 设置应类似于此图像。

        !["分析器" "配置文件" 选项卡的屏幕截图，AutoProfile 设置为活动](images/netmon-parsers1.png)

    3. 单击“确定”。

Netmon 现在配置为与 USB ETW 跟踪文件一起使用。 有关详细信息，请参阅 [如何在 Netmon 中查看 USB ETW 跟踪](how-to-examining-a-trace-file-by-using-netmon.md)。

## <a name="related-topics"></a>相关主题

[使用 USB ETW](using-usb-etw.md)  
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  
[如何在 Netmon 中打开 ETW 跟踪](how-to-examining-a-trace-file-by-using-netmon.md)  

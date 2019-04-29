---
Description: 本主题介绍安装 Netmon 和 USB ETW 分析程序。
title: 如何安装 Netmon 和 USB ETW 分析程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a7f62cf203e6e0071db1c03d6e93924b4469876
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364797"
---
# <a name="how-to-install-netmon-and-usb-etw-parsers"></a>如何安装 Netmon 和 USB ETW 分析程序

本主题介绍安装 Netmon 和 USB ETW 分析程序。

从 Microsoft 下载中心安装 Netmon，然后安装从 USB ETW 分析器[Windows Driver Kit (WDK)](https://msdn.microsoft.com/windows/hardware/hh852362.aspx)。 Netmon 版本 3.3 和更高版本中支持 USB ETW 分析程序。

## <a name="to-install-the-netmon-tool-and-the-netmon-usb-parser"></a>若要安装 Netmon 工具和 Netmon USB 分析器

1. 确定你的计算机是否正在运行 32 位 Windows 或 64 位 Windows:

    1. 打开**启动**菜单中，右键单击**计算机**并查看**属性**。
    2. 看看**系统类型**字段。

    如果您的系统类型是 32 位操作系统，则将使用 x86 下载。 如果您的系统类型是 64 位操作系统，您的处理器是 Itanium，将使用 ia64 下载。 对于其他处理器类型中，使用 x64 或 AMD64 下载。

2. 安装网络监视器：
    1. 上[Windows 网络监视器](https://go.microsoft.com/fwlink/p/?linkid=103158)在 Microsoft 下载中心页上，并阅读工具的说明。
    2. 下**此下载中的文件**推向页面底部的部分中，单击**下载**按钮为您的系统类型。
    3. 下载并运行.exe 文件，以启动安装向导。
    4. 选择**典型**时需要选择安装类型。

3. 安装从 WDK [Windows 驱动程序工具包 8](https://msdn.microsoft.com/windows/hardware/hh852362.aspx)。
4. 允许执行 PowerShell 脚本：
    1. 在开始屏幕中，键入"powershell"，Windows PowerShell 结果中，右键单击并选择**以管理员身份运行**。
    2. 在 PowerShell 窗口中，键入以下命令：

        ```syntax
        Set-ExecutionPolicy RemoteSigned -Force
        ```

    3. 关闭 PowerShell 窗口。
    4. 打开 PowerShell 窗口 (不需要**以管理员身份运行**) 并运行以下命令。 如果该工具包安装到其他位置，请调整路径：

        ```syntax
        cd "C:\Program Files (x86)\Windows Kits\8.0\Tools\x86\Network Monitor Parsers\usb"
        ..\NplAutoProfile.ps1
        ```

    5. 重新启动网络监视器以应用更改。

5. 验证配置文件是 Netmon 中处于活动状态。
    1. 上**工具**菜单中，选择**选项**。
    2. 上**分析器配置文件**选项卡上，请确保 **（生成） 的模板**设置为活动状态。 你的设置应类似于此映像。

        ![设置为活动模板分析程序配置文件选项卡的屏幕截图](images/netmon-parsers1.png)

    3. 单击 **“确定”**。

使用 USB ETW 跟踪文件，现在使用 Netmon 已配置。 有关详细信息，请参阅[如何在网络监视器中查看 USB ETW 跟踪](how-to-examining-a-trace-file-by-using-netmon.md)。

## <a name="related-topics"></a>相关主题

[使用 USB ETW](using-usb-etw.md)  
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  
[如何在网络监视器中打开 ETW 跟踪](how-to-examining-a-trace-file-by-using-netmon.md)  

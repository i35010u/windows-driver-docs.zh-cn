---
title: 下载 Windows 驱动程序工具包 (WDK)
description: 下载最新版本的 Windows 驱动程序工具包 (WDK) 的说明
ms.assetid: 7b5e253b-3bcd-41e3-a646-0f95ce416f87
keywords:
- Windows 驱动程序工具包 (WDK)
- WDK
- 下载
- 驱动程序
ms.date: 08/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: ec30a1b0ac4711f6170c1bf30fa1f0a9e9d0d1e4
ms.sourcegitcommit: 20109e8686f33fd3d683fc1c253b17bfeac0e0c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "56518558"
---
# <a name="download-the-windows-driver-kit-wdk"></a>下载 Windows 驱动程序工具包 (WDK)

WDK 用于开发、测试和部署 Windows 驱动程序。 下面提供了 WDK 的最新公共版本。 

加入 Windows 预览体验计划以获取[WDK Insider Preview 版本](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)。 有关 Windows Insider Preview 版本的安装说明，请参阅[安装 Windows 驱动程序工具包 (WDK) 的预览版本](installing-preview-versions-wdk.md)。

* [了解驱动程序开发中的新增内容](what-s-new-in-driver-development.md) 
* [查看已知问题](https://go.microsoft.com/fwlink/?linkid=872986)

## <a name="wdk-for-windows-10-version-1809"></a>适用于 Windows 10 版本 1809 的 WDK

### <a name="download-iconimagesdownload-installpng-step-1-install-visual-studio-2017"></a>![“下载”图标](images/download-install.png) 第 1 步：安装 Visual Studio 2017 
以下版本的 Visual Studio 2017 支持驱动程序开发： 

* [下载 Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)
* [下载 Visual Studio Professional 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15) 
* [下载 Visual Studio Enterprise 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15)

安装 Visual Studio 时，选择“使用 C++ 的桌面开发”工作负载。 Windows 10 软件开发工具包 (SDK) 会自动包括在内，并显示在右侧的“摘要”窗格中。 

对于 ARM/ARM64 驱动程序开发，选择“单个组件”，然后在“编译器、生成工具和运行时”下方，选择“适用于 ARM/ARM64 的 Visual C++ 编译器和库”。


### <a name="download-iconimagesdownload-installpng-step-2-install-wdk-for-windows-10-version-1809"></a>![“下载”图标](images/download-install.png) 步骤 2：安装适用于 Windows 10 版本 1809 的 WDK

* [下载适用于 Windows 10 版本 1809 的 WDK](https://go.microsoft.com/fwlink/?linkid=2026156) 

从 1709 版本开始的新功能：默认情况下，安装 WDK 时将安装 WDK Visual Studio 扩展。 必须完成此操作，才能使 WDK VS 集成正常工作。 

## <a name="enterprise-wdk-for-windows-10-version-1809-ewdk"></a>适用于 Windows 10 版本 1809 的企业版 WDK (EWDK) 

EWDK 是一种用于生成驱动程序的独立自包含命令行环境。 其中包括 Visual Studio 生成工具、SDK 和 WDK。  EWDK 的最新公共版本包含 Visual Studio 生成工具 15.8.9。  若要开始使用，请装载 ISO 并运行 **LaunchBuildEnv**。 

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools"></a>![“下载”图标](images/download-install.png) 包含 Visual Studio 生成工具的 EWDK

* [下载适用于 Windows 10 版本 1809 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-EWDK)


## <a name="additional-information"></a>其他信息

### <a name="release-notes-and-run-time-requirements"></a>发行说明和运行时要求

WDK 需要 Visual Studio，有关 Visual Studio 的系统要求的详细信息，请查看 [Visual Studio 2017 系统要求](https://www.visualstudio.com/productinfo/vs2017-system-requirements-vs)。 

EWDK 还额外需要 .NET 4.6.1，有关 .NET 可以在哪些平台上运行的详细信息，请查看 [.NET Framework 系统要求](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)。 

你可以使用 WDK 开发适用于以下操作系统的驱动程序： 

|客户端 OS|服务器 OS|
|-|-|
|Windows 10|Windows Server 2019、Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
Windows 8|Windows Server 2012|
Windows 7|Windows Server 2008 R2 SP1|

### <a name="universal-windows-driver-samples"></a>通用 Windows 驱动程序示例

若要获取通用 Windows 驱动程序示例，请执行以下任一操作： 
* 转到 [GitHub](https://github.com/Microsoft/Windows-driver-samples) 上的驱动程序示例页面，然后单击该页面右侧的“克隆”或“下载”>“下载 ZIP”。 
* 下载[适用于 Visual Studio 的 GitHub 扩展](https://visualstudio.github.com/)以连接到 GitHub 存储库。 
* [了解有关驱动程序示例的新增功能的详细信息](https://developer.microsoft.com/windows/hardware/drivers-code-samples)。 

## <a name="related-downloads"></a>相关下载
* [下载 WDK Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)
* [下载以前版本的 WDK](other-wdk-downloads.md)
* [下载 Windows 评估和部署工具包 (Windows ADK)](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit)
* [下载 Windows HLK、HCK 或徽标工具包](https://developer.microsoft.com/windows/hardware/windows-hardware-lab-kit)
* [下载 Windows 调试工具 (WinDbg)](https://developer.microsoft.com/windows/hardware/download-windbg)
* [下载 Windows 符号程序包](https://developer.microsoft.com/windows/hardware/download-symbols)


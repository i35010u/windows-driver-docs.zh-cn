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
ms.custom: 19H1
ms.openlocfilehash: 92dfee5d72fee1bc49c97ba99b7a5182d1a9201a
ms.sourcegitcommit: a0da18a4c5c636c4980e8ed77c6879e617299580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66373155"
---
# <a name="download-the-windows-driver-kit-wdk"></a>下载 Windows 驱动程序工具包 (WDK)

WDK 用于开发、测试和部署 Windows 驱动程序。 下面提供了 WDK 的最新公共版本。

加入 Windows 预览体验计划以获取[WDK Insider Preview 版本](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)。 有关 Windows Insider Preview 版本的安装说明，请参阅[安装 Windows 驱动程序工具包 (WDK) 的预览版本](installing-preview-versions-wdk.md)。

* [了解驱动程序开发中的新增内容](what-s-new-in-driver-development.md)
* [查看已知问题](https://go.microsoft.com/fwlink/?linkid=872986)

## <a name="wdk-for-windows-10-version-1903"></a>WDK 适用于 Windows 10，版本 1903

### <a name="download-iconimagesdownload-installpng-step-1-install-visual-studio-2019"></a>![“下载”图标](images/download-install.png) 第 1 步：安装 Visual Studio 2019

以下版本的 Visual Studio 2019 支持驱动程序开发：

* [下载 Visual Studio Community 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16)
* [下载 Visual Studio Professional 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=16)
* [下载 Visual Studio Enterprise 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=16)

安装 Visual Studio 时，选择“使用 C++ 的桌面开发”  工作负载。 Windows 10 软件开发工具包 (SDK) 会自动包括在内，并显示在右侧的“摘要”  窗格中。

对于 ARM/ARM64 驱动程序开发，选择“单个组件”  ，然后在“编译器、生成工具和运行时”  下方，选择“适用于 ARM/ARM64 的 Visual C++ 编译器和库”  。

对于每个体系结构，你想要生成的驱动程序，请安装 Spectre 缓解的库通过单个组件-> 编译器、 生成工具，并运行时-> MSVC v142-VS 2019 c + x64/x86 Spectre 缓解库 (v14.21)。 

### <a name="download-iconimagesdownload-installpng-step-2-install-wdk-for-windows-10-version-1903"></a>![“下载”图标](images/download-install.png) 步骤 2：安装 WDK 适用于 Windows 10，版本 1903

* [下载 WDK 适用于 Windows 10，版本 1903](https://go.microsoft.com/fwlink/?linkid=2085767)

从 1709 版本开始的新功能：默认情况下，安装 WDK 时将安装 WDK Visual Studio 扩展。 必须完成此操作，才能使 WDK VS 集成正常工作。

## <a name="enterprise-wdk-for-windows-10-version-1903-ewdk"></a>企业 WDK 适用于 Windows 10，版本 1903 (EWDK)

EWDK 是一种用于生成驱动程序的独立自包含命令行环境。 其中包括 Visual Studio 生成工具、SDK 和 WDK。  EWDK 的最新公共版本包含 Visual Studio 2019 生成工具 16.0.0。  若要开始使用，请装载 ISO 并运行 **LaunchBuildEnv**。

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools"></a>![“下载”图标](images/download-install.png) 包含 Visual Studio 生成工具的 EWDK

* [下载 EWDK 适用于 Windows 10，版本 1903](https://developer.microsoft.com/windows/hardware/license-terms-EWDK-2)

## <a name="additional-information"></a>其他信息

### <a name="release-notes-and-run-time-requirements"></a>发行说明和运行时要求

WDK 需要 Visual Studio 中，有关详细信息的 Visual Studio 系统要求的详细信息，请查看[Visual Studio 2019 系统要求](https://docs.microsoft.com/visualstudio/releases/2019/system-requirements)。

EWDK 此外将什么.NET 的详细信息运行的请评审需要.NET 4.7.2 [.NET Framework 系统需求](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)。

你可以使用 WDK 开发适用于以下操作系统的驱动程序：

|客户端 OS|服务器 OS|
|-|-|
|Windows 10|Windows Server 2019、Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
Windows 8|Windows Server 2012|
Windows 7|Windows Server 2008 R2 SP1|

### <a name="universal-windows-driver-samples"></a>通用 Windows 驱动程序示例

若要获取通用 Windows 驱动程序示例，请执行以下任一操作：

* 转到 [GitHub](https://github.com/Microsoft/Windows-driver-samples) 上的驱动程序示例页面，然后单击该页面右侧的“克隆”或“下载”>“下载 ZIP”  。
* 下载[适用于 Visual Studio 的 GitHub 扩展](https://visualstudio.github.com/)以连接到 GitHub 存储库。
* [了解有关驱动程序示例的新增功能的详细信息](https://developer.microsoft.com/windows/hardware/drivers-code-samples)。

## <a name="related-downloads"></a>相关下载

* [下载 WDK Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)
* [下载以前版本的 WDK](other-wdk-downloads.md)
* [下载 Windows 评估和部署工具包 (Windows ADK)](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit)
* [下载 Windows HLK、HCK 或徽标工具包](https://developer.microsoft.com/windows/hardware/windows-hardware-lab-kit)
* [下载 Windows 调试工具 (WinDbg)](https://developer.microsoft.com/windows/hardware/download-windbg)
* [下载 Windows 符号程序包](https://developer.microsoft.com/windows/hardware/download-symbols)

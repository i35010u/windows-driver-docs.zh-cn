---
title: 下载 Windows 驱动程序工具包 (WDK)
description: 下载最新版本的 Windows 驱动程序工具包 (WDK) 的说明
ms.assetid: 7b5e253b-3bcd-41e3-a646-0f95ce416f87
keywords:
- Windows 驱动程序工具包 (WDK)
- WDK
- 下载
- 驱动程序
ms.date: 03/16/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: fb64e0e87ad62c4da101f066378d17f48002a2ca
ms.sourcegitcommit: 3794904c6f741bdc407dfe22341080646602f972
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "80807614"
---
# <a name="download-the-windows-driver-kit-wdk"></a>下载 Windows 驱动程序工具包 (WDK)

WDK 用于开发、测试和部署 Windows 驱动程序。

* [了解驱动程序开发中的新增内容](what-s-new-in-driver-development.md)
* [查看已知问题](https://go.microsoft.com/fwlink/?linkid=872986)

加入 Windows 预览体验计划以获取[WDK Insider Preview 版本](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)。 有关 Windows Insider Preview 版本的安装说明，请参阅[安装 Windows 驱动程序工具包 (WDK) 的预览版本](installing-preview-versions-wdk.md)。

## <a name="wdk-for-windows-10-version-1903"></a>适用于 Windows 10 版本 1903 的 WDK

### <a name="download-icon-step-1-install-visual-studio-2019"></a>![“下载”图标](images/download-install.png) 步骤 1：安装 Visual Studio 2019

WDK 需要 Visual Studio。 有关 Visual Studio 系统要求的详细信息，请参阅 [Visual Studio 2019 系统要求](https://docs.microsoft.com/visualstudio/releases/2019/system-requirements)。 

以下版本的 Visual Studio 2019 支持针对此发行版进行驱动程序开发：

* [下载 Visual Studio Community 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16)
* [下载 Visual Studio Professional 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=16)
* [下载 Visual Studio Enterprise 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=16)

安装 Visual Studio 2019 时，选择“使用 C++ 的桌面开发”  工作负荷。 Windows 10 软件开发工具包 (SDK) 会自动包括在内，并显示在右侧的“摘要”  窗格中。 请注意，与适用于 Windows 10 版本 1903 的 WDK 兼容的 SDK 版本可能不是默认的 SDK。 若要选择正确的 SDK：

1. 在“Visual Studio 安装程序”中“工作负荷”选项卡上的“安装详细信息”下，展开“通用 Windows 平台开发”。    
1. 在“可选”下，选择“Windows 10 SDK (10.0.18362.0)”。  
1. 继续安装。

如果已安装 Visual Studio 2019，则可以使用 Visual Studio 安装程序中的“修改”按钮安装 Windows 10 SDK (10.0.18362.0)。 

通过执行以下操作，验证是否已安装了适用于 x86/x64 的 MSVC v142 生成工具的正确版本 
1. 选择“单个组件” 
1. 在“编译器、生成工具和运行时”  下，选项“MSVC v142 C++ -VS 2019 x64/x86 生成工具(v14.21)”  应处于选中状态，如果没有，请将其选中。
1. 如果已安装 MSVC 生成工具的更高版本，则需在 VS 的项目属性中设置 MSVC 版本。 请转到“配置属性”>“高级”，然后将“MSVC 工具集版本”设置为“14.21.XXXX”。     如果要使用命令行，请单击此 [VS 链接](https://docs.microsoft.com/cpp/build/building-on-the-command-line?view=vs-2019)。

对于 ARM/ARM64 驱动程序开发： 

1. 选择“单个组件”  。 
1. 在“编译器、生成工具和运行时”  下，选择“MSVC v142 - VS 2019 C++ ARM 生成工具(v14.21)”  和“MSVC v142 - VS 2019 C++ ARM64 生成工具(v14.21)”  。

需要为要生成驱动程序的每个体系结构安装 Spectre 缓解库。 转到“单个组件”  选项卡，在“编译器、生成工具和运行时”标题下  ：
  * 对于 x86 和 x64，请选择“MSVC v142 - VS 2019 C++ x64/x86 Spectre 缓解库(v14.21)”  。
  * 对于 ARM，请选择“MSVC v142 - VS 2019 C++ ARM Spectre 缓解库(v14.21)”。 
  * 对于 ARM64，请选择“MSVC v142 - VS 2019 C++ ARM64 Spectre 缓解库(v14.21)”。 

### <a name="download-icon-step-2-install-wdk-for-windows-10-version-1903"></a>![“下载”图标](images/download-install.png) 步骤 2：安装适用于 Windows 10 版本 1903 的 WDK

* [下载适用于 Windows 10 版本 1903 的 WDK](https://go.microsoft.com/fwlink/?linkid=2085767)

默认情况下，安装 WDK 时将安装 WDK Visual Studio 扩展。 

## <a name="enterprise-wdk-ewdk-for-windows-10-version-1903"></a>适用于 Windows 10 版本 1903 的企业版 WDK (EWDK)

EWDK 是一种用于生成驱动程序的独立自包含命令行环境。 其中包括 Visual Studio 生成工具、SDK 和 WDK。  EWDK 的最新公共版本包含 Visual Studio 1903 生成工具 16.0.0。  若要开始使用，请装载 ISO 并运行 **LaunchBuildEnv**。

EWDK 还需要 .NET Framework 版本 4.7.2。 有关 .NET Framework 的其他要求的详细信息，请参阅 [.NET Framework 系统要求](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)。

### <a name="download-icon-ewdk-with-visual-studio-build-tools"></a>![“下载”图标](images/download-install.png) 包含 Visual Studio 生成工具的 EWDK

* [下载适用于 Windows 10 版本 1903 的 EWDK](https://docs.microsoft.com/legal/windows/hardware/enterprise-wdk-license-2019)

## <a name="additional-information"></a>附加信息

### <a name="release-notes-and-runtime-requirements"></a>发行说明和运行时要求

你可以使用 WDK 开发适用于以下操作系统的驱动程序：

|客户端 OS|服务器 OS|
|-|-|
|Windows 10|Windows Server 2019、Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
Windows 8|Windows Server 2012|
Windows 7|Windows Server 2008 R2 SP1|

### <a name="universal-windows-driver-samples"></a>通用 Windows 驱动程序示例

若要下载通用 Windows 驱动程序示例，请执行以下任一操作：

* 转到 [GitHub](https://github.com/Microsoft/Windows-driver-samples) 上的驱动程序示例页面，然后依次单击“克隆或下载”、“下载 ZIP”   。
* 下载[适用于 Visual Studio 的 GitHub 扩展](https://visualstudio.github.com/)，然后连接到 GitHub 存储库。
* 浏览 [Microsoft 示例门户](https://docs.microsoft.com/samples/browse/?products=windows-wdk)中的驱动程序示例。

## <a name="related-downloads"></a>相关下载

* [下载 WDK Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)
* [下载以前版本的 WDK](other-wdk-downloads.md)
* [下载 Windows 评估和部署工具包 (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install)
* [下载 Windows HLK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)
* [下载 Windows 调试工具 (WinDbg)](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)
* [下载 Windows 符号程序包](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols)

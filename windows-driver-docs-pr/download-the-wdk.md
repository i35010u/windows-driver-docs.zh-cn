---
title: 下载 Windows 驱动程序工具包 (WDK)
description: 下载最新版本的 Windows 驱动程序工具包 (WDK) 的说明
ms.assetid: 7b5e253b-3bcd-41e3-a646-0f95ce416f87
keywords:
- Windows 驱动程序工具包 (WDK)
- WDK
- 下载
- 驱动程序
ms.date: 08/17/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a58d05028add8238c6bdbbb029eb6fcb0b4ba51f
ms.sourcegitcommit: f7512f0c18a66672736c8eb87e346d8eb6a71439
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92174188"
---
# <a name="download-the-windows-driver-kit-wdk"></a>下载 Windows 驱动程序工具包 (WDK)

WDK 用于开发、测试和部署 Windows 驱动程序。

* [了解驱动程序开发中的新增内容](what-s-new-in-driver-development.md)
* [查看已知问题](https://go.microsoft.com/fwlink/?linkid=872986)

[加入 Windows 预览体验计划](https://insider.windows.com/)以获取 [WDK Insider Preview 版本](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)。 有关 Windows Insider Preview 版本的安装说明，请参阅[安装 Windows 驱动程序工具包 (WDK) 的预览版本](installing-preview-versions-wdk.md)。

## <a name="runtime-requirements"></a>运行时要求

可以在 Windows 7 及更高版本上运行 Windows 10 版本 2004 WDK，并使用它来开发这些操作系统的驱动程序：

|客户端 OS|服务器 OS|
|-|-|
|Windows 10|Windows Server 2019、Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
Windows 8|Windows Server 2012|
Windows 7|Windows Server 2008 R2 SP1|

## <a name="wdk-for-windows-10-version-2004"></a>适用于 Windows 10 版本 2004 的 WDK

### <a name="download-icon-step-1-install-visual-studio-2019"></a>![“下载”图标](images/download-install.png) 步骤 1：安装 Visual Studio 2019

WDK 需要 Visual Studio。 有关 Visual Studio 系统要求的详细信息，请参阅 [Visual Studio 2019 系统要求](/visualstudio/releases/2019/system-requirements)。

以下版本的 Visual Studio 2019 支持针对此发行版进行驱动程序开发：

* [下载 Visual Studio Community 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16)
* [下载 Visual Studio Professional 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=16)
* [下载 Visual Studio Enterprise 2019](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=16)

安装 Visual Studio 2019 时，选择“使用 C++ 的桌面开发”工作负荷。 Windows 10 软件开发工具包 (SDK) 会自动包括在内，并显示在右侧的“摘要”窗格中。 请注意，与适用于 Windows 10 版本 2004 的 WDK 兼容的 SDK 版本可能不是默认的 SDK。 若要选择正确的 SDK：

在 Visual Studio 安装程序中的“单个组件”选项卡上，搜索“Windows 10 SDK (10.0.19041.0)”，选择此版本，然后继续安装。 请注意，Visual Studio 将在计算机上自动安装 Windows 10 SDK (10.0.19041.1)。

如果已安装 Visual Studio 2019，则可以使用 Visual Studio 安装中的“修改”按钮来安装 Windows 10 SDK (10.0.19041.1)。

WDK 默认启用了 Spectre 缓解，但需要为要开发的每个体系结构将 Spectre 缓解库安装在 Visual Studio 中。 此外，开发适用于 ARM/ARM64 的驱动程序还需要这些体系结构的生成工具也安装在 Visual Studio 中。 若要查找这些项，需要知道系统上安装的 MSVC 的最新版本。

若要查找系统上安装的最新版 MSVC，请在 Visual Studio 安装程序中转到“工作负荷”页，在右侧窗格的“安装详细信息”下展开“使用 C++ 的桌面开发”，然后找到“MSVC v142 - VS 2019 C++ x64/x86 生成工具(V14.xx)”（请注意，其中的 xx 应该就是可用的最高版本）。

有了此信息 (v14.xx)，转到“单个组件”，然后搜索“v14.xx”。 这会返回所有体系结构的工具集，包括 Spectre 缓解库。 选择要为其开发的驱动程序体系结构。

例如，搜索 v14.25 返回以下内容：

```console
MSVC v142 - VS 2019 C++ ARM build tools (v14.25)
MSVC v142 - VS 2019 C++ ARM Spectre-mitigated libs (v14.25)
MSVC v142 - VS 2019 C++ ARM64 build tools (v14.25)
MSVC v142 - VS 2019 C++ ARM64 Spectre-mitigated libs (v14.25)
MSVC v142 - VS 2019 C++ x64/x86 build tools (v14.25)
MSVC v142 - VS 2019 C++ x64/x86 Spectre-mitigated libs (v14.25)
```

### <a name="download-icon-step-2-install-wdk-for-windows-10-version-2004"></a>![“下载”图标](images/download-install.png) 步骤 2：安装适用于 Windows 10 版本 2004 的 WDK

* [下载适用于 Windows 10 版本 2004 的 WDK](https://go.microsoft.com/fwlink/?linkid=2128854)

WDK Visual Studio 扩展包含在默认 WDK 安装中。

## <a name="enterprise-wdk-ewdk-for-windows-10-version-2004"></a>适用于 Windows 10 版本 2004 的企业版 WDK (EWDK)

EWDK 是一种用于生成驱动程序的独立自包含命令行环境。 其中包括 Visual Studio 生成工具、SDK 和 WDK。  EWDK 的最新公共版本包含 Visual Studio 2019 生成工具 16.3.0 和 MSVC 工具集 v14.23。  若要开始使用，请装载 ISO 并运行 **LaunchBuildEnv** 。

EWDK 还需要 .NET Framework 版本 4.7.2。 有关 .NET Framework 的其他要求的详细信息，请参阅 [.NET Framework 系统要求](/dotnet/framework/get-started/system-requirements)。

### <a name="download-icon-ewdk-with-visual-studio-build-tools"></a>![“下载”图标](images/download-install.png) 包含 Visual Studio 生成工具的 EWDK

* [下载适用于 Windows 10 版本 2004 的 EWDK](/legal/windows/hardware/enterprise-wdk-license-2019)

> 你可以将 Visual Studio 界面与 EWDK 中提供的生成工具结合使用。
>
>1. 装载 EWDK ISO。
>2. 运行 `LaunchBuildEnv.cmd`。
>3. 在步骤 2 中创建的环境中，键入“SetupVSEnv”，然后按“Enter” 。
>4. 使用完整的文件路径，从同一环境中启动 devenv.exe。 
>示例： `C:\Program Files (x86)\Microsoft Visual Studio\2019\\%Community|Professionial|Enterprise%\Common7\IDE\devenv.exe`
>
>请注意，Visual Studio 主要版本应与 EWDK 中的版本匹配。 例如，Visual Studio 2019 适用于包含 VS16.X 生成工具的 EWDK。 



## <a name="driver-samples-for-windows-10"></a>Windows 10 驱动程序示例

要下载驱动程序示例，请执行以下任一操作：

* 转到 [GitHub](https://github.com/Microsoft/Windows-driver-samples) 上的驱动程序示例页面，然后依次单击“克隆或下载”、“下载 ZIP” 。
* 下载[适用于 Visual Studio 的 GitHub 扩展](https://visualstudio.github.com/)，然后连接到 GitHub 存储库。
* 浏览 [Microsoft 示例门户](/samples/browse/?products=windows-wdk)中的驱动程序示例。

## <a name="related-downloads"></a>相关下载

* [下载 WDK Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)
* [下载以前版本的 WDK](other-wdk-downloads.md)
* [下载 Windows 评估和部署工具包 (Windows ADK)](/windows-hardware/get-started/adk-install)
* [下载 Windows HLK](/windows-hardware/test/hlk/windows-hardware-lab-kit)
* [下载 Windows 调试工具 (WinDbg)](./debugger/debugger-download-tools.md)
* [下载 Windows 符号程序包](./debugger/debugger-download-symbols.md)

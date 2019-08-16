---
title: 以前的 WDK 版本和其他下载
description: 安装 Windows 驱动程序工具包 (WDK)、Windows 调试器 (WinDBG) 和其他工具的版本。
ms.assetid: e07d9f05-f8d0-46e5-82e6-c23baa614bb1
keywords:
- Windows 驱动程序工具包 (WDK)
- 以前的版本
- WDK
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 44158f2c619b4ede0cb4edfccdfe01e4669aa861
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385992"
---
# <a name="other-wdk-downloads"></a>其他 WDK 下载

本主题介绍 Windows 驱动程序工具包 (WDK) 和企业版 WDK (EWDK) 的早期版本以及用于提供支持的其他下载内容。 若要开发驱动程序，请使用在[下载 Windows 驱动程序工具包 (WDK)](download-the-wdk.md) 上提供下载的最新公共版 Windows 驱动程序工具包 (WDK) 和工具。

Windows 驱动程序工具包 (WDK) 可用于开发、测试和部署 Windows 驱动程序。 若要开发驱动程序，请使用在[下载 Windows 驱动程序工具包 (WDK)](download-the-wdk.md) 上提供下载的最新公共版 Windows 驱动程序工具包 (WDK) 和工具。

本主题介绍 WDK 和企业版 WDK (EWDK) 的早期版本以及用于提供支持的其他下载内容。 若要使用这些早期的版本，必须*先*安装适用于目标平台的 Visual Studio 版本。

## <a name="step-1-install-visual-studio"></a>第 1 步：安装 Visual Studio

支持开发特定 Visual Studio 版本的驱动程序。 若要开发特定 Windows 版本的驱动程序，必须使用在下表中标识（并提供下载链接）的某个 Visual Studio 版本。

| Windows 目标版本      | Visual Studio 版本            |
|--------------------------|----------------------------------------|
| Windows 10 版本 1809 <br/>Windows 10 版本 1803 <br/>Windows 10 版本 1709 | [Visual Studio Community 2017](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15) <br/>[Visual Studio Professional 2017](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15) <br/>[Visual Studio Enterprise 2017](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15) |
| Windows 10 版本 1703 <br/>Windows 10 版本 1607 | [Visual Studio Express 2015 桌面版](https://go.microsoft.com/fwlink/?linkid=875331) <br/>[Visual Studio Community 2015](https://go.microsoft.com/fwlink/p/?LinkId=534599) <br/>[Visual Studio Professional 2015](https://go.microsoft.com/fwlink/p/?LinkId=619628) <br/>[Visual Studio Enterprise 2015](https://go.microsoft.com/fwlink/p/?LinkId=619629) |
| Windows 8.1 更新 <br/>Windows 8.1 | [Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=875331) |
| Windows 8                | [Visual Studio Professional 2012](https://go.microsoft.com/fwlink/p/?LinkID=255976) <br/>[Visual Studio Ultimate 2012](https://go.microsoft.com/fwlink/p/?LinkID=255982) |

### <a name="configure-visual-studio-for-windows-10-versions-1709-1803-and-1809"></a>配置适用于 Windows 10 版本 1709、1803 和 1809 的 Visual Studio

安装 Visual Studio 时，选择“使用 C++ 的桌面开发”  工作负载。 Windows 10 软件开发工具包 (SDK) 会自动包括在内，并显示在右侧的“摘要”  窗格中。

若要开发 ARM/ARM64 的驱动程序，请选择“单个组件”  ，然后在“编译器、生成工具和运行时”  下选择“适用于 ARM/ARM64 的 Visual C++ 编译器和库”  。

### <a name="install-the-windows-sdk-to-target-windows-10-versions-1607-and-1703"></a>将 Windows SDK 安装到目标 Windows 10 版本 1607 和 1703

如果开发的目标系统运行 Windows 10 版本 1607 或 Windows 10 版本 1703，则应安装 Visual Studio 2015，然后再下载并安装适用于目标 Windows 10 版本的 Windows SDK 版本，如下表所示。

| Windows 目标版本      | Windows SDK 版本            |
|--------------------------|----------------------------------------|
| Windows 10 版本 1703 | [适用于 Windows 10.0.15063.468 的 Windows SDK](https://go.microsoft.com/fwlink/p/?LinkID=845298) |
| Windows 10 版本 1607 | [适用于 Windows 10.0.14393.795 的 Windows SDK](https://go.microsoft.com/fwlink/p/?LinkId=838916) |
| Windows 8.1              | [适用于 Windows 8.1 的 Windows SDK](https://go.microsoft.com/fwlink/p/?LinkId=323507) |
| Windows 8                | [适用于 Windows 8 的 Windows SDK](https://go.microsoft.com/fwlink/p/?LinkId=226658) |

Windows SDK 未包含在 Visual Studio 2015 中，因此必须单独安装 SDK。 更高版本的 Visual Studio 包含 Windows SDK。

## <a name="step-2-install-the-wdk"></a>步骤 2：安装 WDK

WDK 与 Visual Studio 和 Windows 调试工具 (WinDbg) 集成在一起。 此集成环境提供了开发、生成、打包、部署、测试和调试驱动程序所需的工具。

> [!Note]
> 从 Windows 10 版本 1709 开始，安装 WDK 时会默认安装 Visual Studio 的 WDK 扩展。 这些扩展是将 WDK 与 Visual Studio 集成所必需的。

| Windows 版本      | WDK 和相关下载                       |
|--------------------------|-------------------------------------------------|
| Windows 10 版本 1809 | [适用于 Windows 10 版本 1809 的 WDK](https://go.microsoft.com/fwlink/?linkid=2026156) |
| Windows 10 版本 1803 | [适用于 Windows 10 版本 1803 的 WDK](https://go.microsoft.com/fwlink/?linkid=873060) |
| Windows 10 版本 1709 | [适用于 Windows 10 版本 1709 的 WDK](https://go.microsoft.com/fwlink/p/?linkid=859232) |
| Windows 10 版本 1703 | [适用于 Windows 10 版本 1703 的 WDK](https://go.microsoft.com/fwlink/p/?LinkID=845980) |
| Windows 10 版本 1607 | [适用于 Windows 10 版本 1607 的 WDK](https://go.microsoft.com/fwlink/p/?LinkId=526733)                |
| Windows 8.1 更新       | [WDK 8.1 更新](https://go.microsoft.com/fwlink/p/?LinkId=393659)（仅英语） <br/>[WDK 8.1 更新测试包](https://go.microsoft.com/fwlink/p/?LinkID=393660)（仅英语） <br/>[WDK 8.1 示例](https://code.msdn.microsoft.com/windowshardware/Windows-Driver-Kit-WDK-81-cf35e953) |
| Windows 8                | [WDK 8](https://go.microsoft.com/fwlink/p/?LinkID=324284)（仅英语） <br/>[WDK 8 可再发行组件](https://go.microsoft.com/fwlink/p/?LinkID=253170)（仅英语） <br/>[WDK 8 示例](https://code.msdn.microsoft.com/windowshardware/Windows-Driver-Kit-WDK-80-e3161626) |
| Windows XP <br/>Windows Server 2003 | [WDK 7.1.0](https://www.microsoft.com/download/confirmation.aspx?id=11800) |


> [!IMPORTANT]
> 如果在已安装适用于 Windows 10 版本 1607 的 WDK 的系统上安装了适用于 Windows 10 版本 1703 的 WDK，则可能会删除 WDK 早期版本的某些文件。 若要还原这些文件，请执行以下操作：
> 1. 在“开始”菜单上，在搜索框中输入“应用和功能”  ，然后从结果中选择“应用和功能”  。
> 2. 在“应用和功能”  列表中查找“Windows 驱动程序工具包 - Windows 10.0.15063.0”  ，然后选择该程序。
> 3. 依次选择“修改”  >“修复”  ，然后按照屏幕上的说明进行操作。
> 4. 此时这些文件将被还原。

## <a name="optional-install-the-ewdk"></a>可选：安装 EWDK

企业版 WDK (EWDK) 是一种独立的自包含命令行环境，用于生成驱动程序和基本的 Win32 测试应用程序。 其中包括 Visual Studio 生成工具、SDK 和 WDK。 此环境不包含在 Visual Studio 中可用的所有功能，例如集成开发环境 (IDE)。

使用 EWDK 需要 .NET Framework 4.6.1。 若要详细了解哪些系统运行此版本的框架，请参阅 [.NET Framework 系统要求](https://docs.microsoft.com/en-us/dotnet/framework/get-started/system-requirements)。 如需用于下载 .NET Framework 的链接，请参阅[安装面向开发人员的 .NET Framework](https://docs.microsoft.com/en-us/dotnet/framework/install/guide-for-developers)。

有关 EWDK 的详细信息，请参阅[使用企业版 WDK 10](https://docs.microsoft.com/en-us/windows-hardware/drivers/develop/using-the-enterprise-wdk)。

| Windows 版本               | EWDK                              |
|-----------------------------------|-----------------------------------|
| Windows 10 版本 1809          | [适用于 Windows 10 版本 1809 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-EWDK) |
| Windows 10 版本 1803          | [适用于 Windows 10 版本 1803 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-EWDK) |
| Windows 10 版本 1709          | [适用于 Visual Studio 与生成工具 15.6 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-EWDK)（推荐） <br/>[适用于 Visual Studio 与生成工具 15.4 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-EWDK) <br/>[适用于 Visual Studio 与生成工具 15.2 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-EWDK) |
| Windows 10 版本 1703          | [适用于 Windows 10 版本 1703 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk) |

> [!Note]
> 从 Windows 10 版本 1709 开始，EWDK 基于 ISO。 若要开始使用，请下载并装载 ISO，然后运行 **LaunchBuildEnv**。

## <a name="optional-install-updated-test-certificates-for-hal-extensions"></a>可选：安装适用于 HAL 扩展的已更新测试证书

若要使用 HAL 扩展，请准备好运行 Windows 10 版本 1709 或更高版本的 Windows 10 的开发系统。 另请安装 WDK 或 EWDK，然后安装可以作为 ZIP 文件下载的更新版 **Windows OEM HAL 扩展测试证书 2017（仅测试）** ：[HAL_Extension_Test_Cert_2017.zip](https://go.microsoft.com/fwlink/?linkid=872294)。

若要详细了解如何使用此更新的证书，请参阅 Windows 支持上的[“Windows OEM HAL 扩展测试证书 2017（仅测试）”测试证书更新](https://support.microsoft.com/help/4131991/update-for-windows-oem-hal-extension-test-cert-2017-test-only-test-cer)。

## <a name="optional-install-windbg-preview"></a>可选：安装 WinDbg Preview

WinDbg Preview 是 WinDbg 的新版本，在重要位置构建有可扩展的调试器数据模型，具有更现代的视觉效果、更快速的 Windows 和成熟的脚本体验。 WinDbg Preview 支持调试每个版本的 Windows 10。

如需 WinDbg Preview 的下载链接和详细信息，请参阅[下载 WinDbg Preview](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools#small-windbg-preview-logo-download-windbg-preview)。

## <a name="standalone-tools-for-debugging-windows-xp-and-windows-vista"></a>用于调试 Windows XP 和 Windows Vista 的独立工具

如果你要调试 Windows XP、Windows Server 2003、Windows Vista 或 Windows Server 2008（或者使用这些操作系统之一来运行 Windows 调试工具），则需要使用这些调试工具的 Windows 7 版本。 它包含在适用于 Windows 7 和 .NET Framework 4.0 的 SDK 中。

> [!IMPORTANT]
> 在安装适用于 Windows 7 的 SDK 时，更高版本的 Visual C++ 2010 可再发行组件可能会引发问题。 有关详细信息，请参阅 Microsoft 支持上的 [Windows SDK Fails to Install with Return Code 5100](https://support.microsoft.com/en-us/help/2717426/windows-sdk-fails-to-install-with-return-code-5100)（Windows SDK 无法安装，返回代码为 5100）。

获取适用于 Windows XP 的独立调试工具的方法是先下载 Windows 7 SDK：[适用于 Windows 7 和 .NET Framework 4 的 Microsoft Windows SDK](https://www.microsoft.com/download/confirmation.aspx?id=8279)。

若要将 Windows 调试工具作为单独组件进行安装，请启动 SDK 安装程序，在安装向导中选择“Windows 调试工具”  ，然后清除其他所有组件。

### <a name="related-downloads"></a>相关下载
* [下载 Windows 评估和部署工具包 (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install)
* [下载 Windows HLK、HCK 或徽标工具包](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)
* [下载 Windows 调试工具 (WinDbg)](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)
* [下载 Windows 符号程序包](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols)
* [下载 WDK Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)

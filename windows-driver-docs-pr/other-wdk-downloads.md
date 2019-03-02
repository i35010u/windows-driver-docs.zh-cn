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
ms.openlocfilehash: 0515bb2812a30a27c8f6a5c5d0a2c69a10777c3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518502"
---
# <a name="other-wdk-downloads"></a>其他 WDK 下载

使用 [Windows 驱动程序工具包 (WDK) 和工具的最新公共版本](download-the-wdk.md)来开发驱动程序。 本主题包含有关以前版本的 WDK 以及用于提供支持的其他下载的信息。


## <a name="wdk-for-windows-10-version-1803"></a>适用于 Windows 10 版本 1803 的 WDK

### <a name="download-iconimagesdownload-installpng-step-1-install-visual-studio-2017"></a>![“下载”图标](images/download-install.png) 第 1 步：安装 Visual Studio 2017 
以下版本的 Visual Studio 2017 支持驱动程序开发： 

* [下载 Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)
* [下载 Visual Studio Professional 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15) 
* [下载 Visual Studio Enterprise 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15)

安装 Visual Studio 时，选择“使用 C++ 的桌面开发”工作负载。 Windows 10 软件开发工具包 (SDK) 会自动包括在内，并显示在右侧的“摘要”窗格中。 

对于 ARM/ARM64 驱动程序开发，选择“单个组件”，然后在“编译器、生成工具和运行时”下方，选择“适用于 ARM/ARM64 的 Visual C++ 编译器和库”。


### <a name="download-iconimagesdownload-installpng-step-2-install-wdk-for-windows-10-version-1803"></a>![“下载”图标](images/download-install.png) 步骤 2：安装适用于 Windows 10 版本 1803 的 WDK

* [下载适用于 Windows 10 版本 1803 的 WDK](https://go.microsoft.com/fwlink/?linkid=873060) 

从 1709 版本开始的新功能：默认情况下，安装 WDK 时将安装 WDK Visual Studio 扩展。 必须完成此操作，才能使 WDK VS 集成正常工作。 

## <a name="enterprise-wdk-for-windows-10-version-1803-ewdk"></a>适用于 Windows 10 版本 1803 的企业版 WDK (EWDK) 

EWDK 是一种用于生成驱动程序的独立自包含命令行环境。 其中包括 Visual Studio 生成工具、SDK 和 WDK。  EWDK 的最新公共版本包含 Visual Studio 生成工具 15.7。 若要开始使用，请装载 ISO 并运行 **LaunchBuildEnv**。 

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools-157"></a>![“下载”图标](images/download-install.png) 包含 Visual Studio 生成工具 15.7 的 EWDK

* [下载适用于 Windows 10 版本 1803 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-EWDK)

## <a name="additional-information"></a>其他信息

### <a name="release-notes-and-run-time-requirements"></a>发行说明和运行时要求

WDK 需要 Visual Studio，有关 Visual Studio 的系统要求的详细信息，请查看 [Visual Studio 2017 系统要求](https://www.visualstudio.com/productinfo/vs2017-system-requirements-vs)。 

EWDK 还额外需要 .NET 4.6.1，有关 .NET 可以在哪些系统上运行的详细信息，请查看 [.NET Framework 系统需求](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)。 

若要使用 HAL 扩展，请在准备好部署环境后下载并安装更新的 [Windows OEM HAL 扩展测试证书 2017（仅测试）](https://go.microsoft.com/fwlink/?linkid=872294)证书。  [了解详细信息](https://support.microsoft.com/help/4131991)


## <a name="wdk-for-windows-10-version-1709"></a>适用于 Windows 10 版本 1709 的 WDK

### <a name="download-iconimagesdownload-installpng-step-1-install-visual-studio-2017"></a>![“下载”图标](images/download-install.png) 第 1 步：安装 Visual Studio 2017 
以下版本的 Visual Studio 2017 支持驱动程序开发： 

* [下载 Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)
* [下载 Visual Studio Professional 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15) 
* [下载 Visual Studio Enterprise 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15)

安装 Visual Studio 时，选择“使用 C++ 的桌面开发”工作负载。 Windows 10 软件开发工具包 (SDK) 会自动包括在内，并显示在右侧的“摘要”窗格中。 

对于 ARM/ARM64 驱动程序开发，选择“单个组件”，然后在“编译器、生成工具和运行时”下方，选择“适用于 ARM/ARM64 的 Visual C++ 编译器和库”。


### <a name="download-iconimagesdownload-installpng-step-2-install-wdk-for-windows-10-version-1709"></a>![“下载”图标](images/download-install.png) 步骤 2：安装适用于 Windows 10 版本 1709 的 WDK

* [下载适用于 Windows 10 版本 1709 的 WDK](https://go.microsoft.com/fwlink/p/?linkid=859232) 

本版本中的新功能：默认情况下，安装 WDK 时将安装 WDK Visual Studio 扩展。 必须完成此操作，才能使 WDK VS 集成正常工作。 

## <a name="enterprise-wdk-for-windows-10-version-1709-ewdk"></a>适用于 Windows 10 版本 1709 的企业版 WDK (EWDK) 

EWDK 是一种用于生成驱动程序的独立自包含命令行环境。 其中包括 Visual Studio 生成工具、SDK 和 WDK。  EWDK 的最新公共版本包含 Visual Studio 生成工具 15.6。 

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools-156-recommended"></a>![“下载”图标](images/download-install.png) 适用于 Visual Studio 生成工具 15.6 的 EWDK（推荐）

* [下载适用于 Windows 10 版本 1709 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1709-VS15-6)

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools-154"></a>![“下载”图标](images/download-install.png) 包含 Visual Studio 生成工具 15.4 的 EWDK

* [下载适用于 Windows 10 版本 1709 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1709-VS15-4)

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools-152"></a>![“下载”图标](images/download-install.png) 适用于 Visual Studio 生成工具 15.2 的 EWDK

* [下载适用于 Windows 10 版本 1709 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1709)

若要开始使用，请装载 ISO 并运行 **LaunchBuildEnv**。

## <a name="wdk-for-windows-10-version-1703"></a>适用于 Windows 10 版本 1703 的 WDK 

### <a name="download-iconimagesdownload-installpng-install-visual-studio-2015"></a>![“下载”图标](images/download-install.png) 安装 Visual Studio 2015

> [!IMPORTANT]
> 适用于 Windows 10 版本 1703 的 WDK 不兼容 Visual Studio 2017。 使用 Visual Studio 2015 和此版本的 WDK 开发驱动程序。 

以下版本的 Visual Studio 2015 支持驱动程序开发。 

* [下载 Visual Studio Express 2015 桌面版](https://go.microsoft.com/fwlink/?linkid=875331)
* [下载 Visual Studio Community 2015](https://go.microsoft.com/fwlink/p/?LinkId=534599)
* [下载 Visual Studio Professional 2015](https://go.microsoft.com/fwlink/p/?LinkId=619628)
* [下载 Visual Studio Enterprise 2015](https://go.microsoft.com/fwlink/p/?LinkId=619629)

### <a name="download-iconimagesdownload-installpng-install-windows-sdk-for-windows-10-version-1703"></a>![“下载”图标](images/download-install.png) 安装适用于 Windows 10 版本 1703 的 Windows SDK 

* [下载适用于 Windows 10 版本 1703 的 Windows SDK](https://go.microsoft.com/fwlink/p/?LinkID=845298)

### <a name="download-iconimagesdownload-installpng-install-wdk-for-windows-10-version-1703"></a>![“下载”图标](images/download-install.png) 安装适用于 Windows 10 版本 1703 的 WDK 

* [下载适用于 Windows 10 版本 1703 的 WDK](https://go.microsoft.com/fwlink/p/?LinkID=845980)

> [!IMPORTANT]
> 如果你安装 WDK，将无法开发现代应用程序。 

> [!IMPORTANT]
> 如果已安装适用于 Windows 10 版本 1607 的 WDK，则当在适用于 Windows 10 版本 1607 的基础上安装适用于 Windows 10 版本 1703 的 WDK 时，部分 WDK 文件将被删除。 若要还原这些文件，请执行以下操作： 
> 1. 在“开始”菜单上，在搜索框中输入“应用和功能”，然后从结果中选择“应用和功能”。 
> 2. 在“应用和功能”列表中查找“Windows 驱动程序工具包 - Windows 10.0.15063.0”，然后选择该程序。 
> 3. 依次选择“修改”>“修复”，然后按照屏幕上的说明进行操作。 
> 4. 此时这些文件将被还原。 

## <a name="download-iconimagesdownload-installpng-ewdk-for-windows-10-version-1703"></a>![“下载”图标](images/download-install.png) 适用于 Windows 10 版本 1703 的 EWDK 

你还可以安装 EWDK，以在命令行生成环境中生成驱动程序和基本 Win32 测试应用程序。 此环境不包含在 Visual Studio 中可用的所有功能，例如集成开发环境 (IDE)，因此你需要使用自主选择的代码编辑器。 

* [了解有关 EWDK 的详细信息](https://go.microsoft.com/fwlink/p/?LinkId=846040)
* [下载适用于 Windows 10 版本 1703 的 EWDK](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1703)


## <a name="download-iconimagesdownload-installpng-wdk-for-windows-10-version-1607"></a>![“下载”图标](images/download-install.png) 适用于 Windows 10 版本 1607 的 WDK

1. 运行 Windows 更新。 
2. 安装最适合你的开发需求的 Visual Studio 2015 版本。 

    * [下载 Visual Studio Express 2015 桌面版](https://go.microsoft.com/fwlink/?linkid=875331)
    * [下载 Visual Studio Community 2015](https://go.microsoft.com/fwlink/p/?LinkId=534599)
    * [下载 Visual Studio Professional 2015](https://go.microsoft.com/fwlink/p/?LinkId=619628)
    * [下载 Visual Studio Enterprise 2015](https://go.microsoft.com/fwlink/p/?LinkId=619629)

3. 在安装过程中，选择“针对 Windows 10 开发人员的典型安装”选项。 
4. 按照提示完成安装。 
5. [安装适用于 Windows 10 版本 1607 的 WDK](https://go.microsoft.com/fwlink/p/?LinkId=526733) 
** 或**
[安装 EWDK 1607](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk)

## <a name="download-iconimagesdownload-installpng-wdk-81-update-for-windows-81-8-and-7-drivers"></a>![“下载”图标](images/download-install.png) WDK 8.1 更新（适用于 Windows 8.1、8 和 7 驱动程序）

WDK 8.1 更新提供了用于为 Windows 8.1 更新、Windows 8.1、Windows 8 和 Windows 7 生成、测试、调试和部署驱动程序的工具。 拥有该 WDK 时，我们建议你安装 WDK 8.1 更新 Test Pack。 它具有针对设备基础功能、图形、映像、移动宽带（CDMA、GSM、WLAN）、传感器和其他实用程序的测试。 

> [!IMPORTANT]
> 安装 WDK 8.1 更新之前，你需要先安装 Visual Studio 2013。 

1. [下载 Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=875331)
2. [下载 WDK 8.1 更新](https://go.microsoft.com/fwlink/p/?LinkId=393659)（仅英语版） 
3. [下载 WDK 8.1 更新 Test Pack](https://go.microsoft.com/fwlink/p/?LinkID=393660)（仅英语版） 
4. [获取适用于 Windows 8.1 的驱动程序示例](https://code.msdn.microsoft.com/windowshardware/Windows-Driver-Kit-WDK-81-cf35e953) 

## <a name="download-iconimagesdownload-installpng-windbg-for-windows-81"></a>![“下载”图标](images/download-install.png) 适用于 Windows 8.1 的 WinDbg
Windows 调试工具 (WinDbg) 包含在 WDK 8.1 更新中，但也可以作为 Windows 8.1 SDK 的独立组件进行安装。 在安装向导中，选择“Windows 调试工具”，然后清除所有其他组件。 

* [获取 Windows 8.1 SDK 中包含的 (WinDbg)](https://go.microsoft.com/fwlink/p/?LinkId=323507)（仅英语版）

## <a name="download-iconimagesdownload-installpng-remote-debugging-client-for-windows-81"></a>![“下载”图标](images/download-install.png) Windows 8.1 远程调试客户端
使用 Windows 远程调试客户端，你可以通过互联网与 Microsoft 开发人员远程协作，以使用内核调试程序调试内核模式故障。 
* [了解详细信息，并准备远程调试。](https://docs.microsoft.com/windows-hardware/drivers/debugger/remote-debugging)
* [下载远程调试客户端](https://go.microsoft.com/fwlink/p/?LinkId=316921)（仅英语版）  

## <a name="download-iconimagesdownload-installpng-wdk-8"></a>![“下载”图标](images/download-install.png) WDK 8
WDK 8 允许将早期版本的驱动程序迁移到 WDK 8.1 更新和 Visual Studio 2013。 Microsoft 不支持 WDK 8，并且不再提供针对此工具包的更新。 应当使用最新版本的 WDK 和 Visual Studio 来生成适用于 Windows 的驱动程序。 

> [!IMPORTANT]
> 必须先安装 [Visual Studio Professional 2012](https://go.microsoft.com/fwlink/p/?LinkID=255976) 或 [Visual Studio Ultimate 2012](https://go.microsoft.com/fwlink/p/?LinkID=255982)，然后再安装 WDK 8。 

1. [下载 WDK 8（仅英语版）](https://go.microsoft.com/fwlink/p/?LinkID=324284)
2. [下载 WDK 8 可再发行组件](https://go.microsoft.com/fwlink/p/?LinkID=253170)（仅英语版） 
3. [获取适用于 Windows 8 的驱动程序示例](https://code.msdn.microsoft.com/windowshardware/Windows-Driver-Kit-WDK-80-e3161626) 

## <a name="download-iconimagesdownload-installpng-wdk-710-for-windows-xp-drivers"></a>![“下载”图标](images/download-install.png) WDK 7.1.0（适用于 Windows XP 驱动程序）
要开发适用于 Windows XP 或 Windows Server 2003 的驱动程序？ WDK 7.1.0 提供了工具、代码示例、文档、编译器、标题和库，可以使用它们创建适用于这些操作系统的驱动程序。 

* [下载 WDK 7.1.0](https://www.microsoft.com/download/confirmation.aspx?id=11800)（仅英语版） 

## <a name="download-iconimagesdownload-installpng-standalone-debugging-tools-for-debugging-windows-xp-and-windows-vista"></a>![“下载”图标](images/download-install.png) 用于调试 Windows XP 和 Windows Vista 的独立调试工具
如果你要调试 Windows XP、Windows Server 2003、Windows Vista 或 Windows Server 2008（或者使用这些操作系统之一来运行 Windows 调试工具），则需要使用这些调试工具的 Windows 7 版本。 它包含在适用于 Windows 7 和 .NET Framework 4.0 的 SDK 中。 若要将适用于 Windows 的调试工具作为单独组件进行安装，请在 SDK 安装向导中选择适用于 Windows 的调试工具，然后清除其他所有组件。 

> [!IMPORTANT]
> 在安装适用于 Windows 7 的 SDK 时，更高版本的 Visual C++ 2010 可再发行组件可能会引发问题。 有关详细信息，请参阅[支持 Windows SDK](https://support.microsoft.com/kb/2717426)。 

* [获取 Windows 7 SDK 中包含的适用于 Windows XP 的独立调试工具](https://www.microsoft.com/download/confirmation.aspx?id=8279) 

## <a name="related-downloads"></a>相关下载
* [下载 Windows 评估和部署工具包 (Windows ADK)](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit)
* [下载 Windows HLK、HCK 或徽标工具包](https://developer.microsoft.com/windows/hardware/windows-hardware-lab-kit) 
* [下载 Windows 调试工具 (WinDbg)](https://developer.microsoft.com/windows/hardware/download-windbg) 
* [下载 Windows 符号程序包](https://developer.microsoft.com/windows/hardware/download-symbols) 
* [下载 WDK Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK) 

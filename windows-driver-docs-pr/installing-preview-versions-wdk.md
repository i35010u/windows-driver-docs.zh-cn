---
title: 安装 Windows 驱动程序工具包 (WDK) 的预览版本
description: 最新预发行版 Windows 驱动程序工具包 (WDK) 的安装说明
keywords:
- Windows 驱动程序工具包 (WDK)
- WDK
- Insider Preview
- 下载
- 驱动程序
ms.author: eliotgra
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: c034286186c88f231f032c2de031c2780ff04eb3
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63339149"
---
# <a name="installing-preview-versions-of-the-windows-driver-kit-wdk"></a>安装 Windows 驱动程序工具包 (WDK) 的预览版本

此页包含 Windows 驱动程序工具包 (WDK) 的 Insider Preview（预发行）版本的安装说明。 最新预发行版本的 WDK 和 EWDK 的下载链接位于 [https://www.microsoft.com/software-download/windowsinsiderpreviewWDK](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)。  

有关最新**发布**版本的 WDK 的信息，请参阅[下载 Windows 驱动程序工具包 (WDK)](download-the-wdk.md)。 若要下载早期版本的 WDK，请参阅[其他 WDK 下载](other-wdk-downloads.md)。  

## <a name="install-windows-driver-kit-wdk-insider-preview"></a>安装 Windows 驱动程序工具包 (WDK) Insider Preview

### <a name="1-install-visual-studio"></a>1.安装 Visual Studio

- WDK 现在支持 Visual Studio 2019。  支持所有版本。  WDK 不再支持 Visual Studio 2017。 
- 从 [https://visualstudio.microsoft.com/vs/preview/](https://visualstudio.microsoft.com/vs/preview/) 下载。 
- 选择工作负荷：使用 C++ 开发。 
- ARM：若要生成 ARM 驱动程序，必须另外安装组件：单个组件 -> 编译器、生成工具和运行时 -> 适用于 ARM 的 Visual C++ 编译器和库。 
- ARM64：目前不受支持。 

### <a name="2-disable-strong-name-validation"></a>2.禁用强名称验证

WDK Visual Studio 扩展目前未进行强名称签名。 从提升的命令提示符运行以下命令以禁用强名称验证： 

```cpp
reg add HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\StrongName\Verification\*,31bf3856ad364e35 /v TestPublicKey /t REG_SZ /d 00240000048000009400000006020000002400005253413100040000010001003f8c902c8fe7ac83af7401b14c1bd103973b26dfafb2b77eda478a2539b979b56ce47f36336741b4ec52bbc51fecd51ba23810cec47070f3e29a2261a2d1d08e4b2b4b457beaa91460055f78cc89f21cd028377af0cc5e6c04699b6856a1e49d5fad3ef16d3c3d6010f40df0a7d6cc2ee11744b5cfb42e0f19a52b8a29dc31b0 /f

reg add HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\StrongName\Verification\*,31bf3856ad364e35 /v TestPublicKey /t REG_SZ /d 00240000048000009400000006020000002400005253413100040000010001003f8c902c8fe7ac83af7401b14c1bd103973b26dfafb2b77eda478a2539b979b56ce47f36336741b4ec52bbc51fecd51ba23810cec47070f3e29a2261a2d1d08e4b2b4b457beaa91460055f78cc89f21cd028377af0cc5e6c04699b6856a1e49d5fad3ef16d3c3d6010f40df0a7d6cc2ee11744b5cfb42e0f19a52b8a29dc31b0 /f 
```

### <a name="3-install-sdk-insider-preview"></a>3.安装 SDK Insider Preview 

[获取 SDK Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)

### <a name="4-install-wdk-insider-preview"></a>4.安装 WDK Insider Preview

[获取 WDK Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)

> [!Note]   
> 在安装过程中，你将看到 Visual Studio 安装程序安装 WDK 的 Visual Studio 扩展。 

## <a name="install-enterprise-wdk-ewdk-insider-preview"></a>安装企业版 WDK (EWDK) Insider Preview

EWDK 是一种用于生成驱动程序的独立自包含命令行环境。  它包括用于 Visual Studio 2019 的生成工具、SDK、WDK 以及对 ARM64 驱动程序开发的支持。 有关详细信息，请参阅[安装企业版 WDK](https://docs.microsoft.com/windows-hardware/drivers/develop/installing-the-enterprise-wdk)。 

[获取企业版 Windows 驱动程序工具包 (WDK) Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)

若要开始使用，请装载 ISO 并单击“LaunchBuildEnv”。 

## <a name="run-time-requirements-for-the-wdk-and-the-ewdk"></a>WDK 和 EWDK 的运行时要求

WDK 需要 Visual Studio。 有关 Visual Studio 系统要求的详细信息，请参阅[Visual Studio 2019 系统要求](https://docs.microsoft.com/visualstudio/releases/2019/system-requirements)。

此外，EWDK 需要 .NET 4.7.2。 有关运行 .NET 的平台的更多信息，请参阅 [.NET Framework 系统要求](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)。

可以使用 WDK Insider Preview 和 EWDK Insider Preview 开发适用于以下操作系统的驱动程序： 

|客户端 OS|服务器 OS|
|---|---|
|Windows 10|Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
|Windows 8|Windows Server 2012|
|Windows 7|Windows Server 2008 R2 SP1|


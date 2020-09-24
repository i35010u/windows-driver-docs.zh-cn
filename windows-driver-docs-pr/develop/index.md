---
ms.assetid: 6e8be17d-6e98-441e-9a2c-e62a007786ee
title: 开发、测试以及部署驱动程序
description: 从 Windows 驱动程序工具包 (WDK) 8 开始，Windows 驱动程序开发环境和调试器已集成到 Microsoft Visual Studio 中。
keywords:
- 开发驱动程序
- 测试驱动程序
- 部署驱动程序
ms.date: 08/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 4204e86a15ad16285ab96575689e5b883f765a14
ms.sourcegitcommit: 0c34101a0eed9f187fec03026021fff89bd233e3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2020
ms.locfileid: "91135178"
---
# <a name="developing-testing-and-deploying-drivers"></a>开发、测试以及部署驱动程序

Windows 驱动程序开发环境和 Windows 调试器已集成到 Microsoft Visual Studio 中。 在此集成的驱动程序开发环境中，Visual Studio 界面中提供有编码、构建、打包、部署和测试驱动程序所需的大部分工具。

若要设置集成开发环境，请先安装 Visual Studio，然后再安装 WDK。 要了解如何获取 Visual Studio 和 WDK，请访问 [WDK 设置和下载页面](../download-the-wdk.md)。 [Windows 调试工具](../debugger/index.md)包含在 WDK 安装中。

WDK 使用 MSBuild.exe，Visual Studio 用户界面中提供有此程序，并且它也可以作为命令行工具提供。 在 Visual Studio 环境中创建的驱动程序使用项目和解决方案文件来描述项目或项目组。 Visual Studio 环境提供有用于将旧源和目录文件转换成项目和解决方案文件的工具。

Visual Studio 环境提供适用于以下项的模板：

- 新驱动程序
- 驱动程序包
- 新测试
- 现有测试的增强功能
- 自定义驱动程序部署脚本

在 Visual Studio 环境中，你可以配置构建流程，使其自动创建和签署驱动程序包。 Visual Studio 中提供了静态和实时分析工具。 你可以配置用于测试驱动程序的目标计算机，并在每次重建时将你的驱动程序自动部署到目标计算机。 你可以从多个运行时测试中进行选择，也可以编写自己的测试。

本部分的主题介绍了如何使用 Visual Studio 执行驱动程序开发、部署和测试中涉及的各任务。

## <a name="additional-videos"></a>其他视频

你将在 Windows 驱动程序文档中的以下页面上找到视频：

- [将 Windows Performance Toolkit (WPT) 与 WDF 配合使用](../wdf/using-the-windows-performance-toolkit--wpt--with-wdf.md)
- [视频：在没有调试程序的情况下访问驱动程序 IFR 日志](../wdf/video--accessing-driver-ifr-logs-without-a-debugger.md)
- [视频：使用 WDF 源代码调试驱动程序](../wdf/video--debugging-your-driver-with-wdf-source-code.md)
- [视频：调试 UMDF 驱动程序](../wdf/videos--debugging-umdf-drivers.md)
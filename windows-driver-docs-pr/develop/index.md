---
ms.assetid: 6e8be17d-6e98-441e-9a2c-e62a007786ee
title: 开发、测试以及部署驱动程序
description: 从 Windows 驱动程序工具包 (WDK) 8 开始，Windows 驱动程序开发环境和调试器已集成到 Microsoft Visual Studio 中。
keywords:
- 开发驱动程序
- 调试驱动程序
- 测试驱动程序
- 部署驱动程序
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 26b7d994d9a027bf20cdc6f322899ae03d1cf381
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56465389"
---
# <a name="developing-testing-and-deploying-drivers"></a>开发、测试以及部署驱动程序

Windows 驱动程序开发环境和 Windows 调试器已集成到 Microsoft Visual Studio 中。 在此集成的驱动程序开发环境中，Visual Studio 界面中提供有编码、构建、打包、部署、调试和测试驱动程序所需的大部分工具。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/9673727b-89ef-4a54-8228-dad41dbd8201]

若要设置集成开发环境，请先安装 Visual Studio，然后再安装 WDK。 可以在[此处](https://go.microsoft.com/fwlink/p/?linkid=239721)找到有关如何获取 Visual Studio 和 WDK 的信息。 安装 WDK 时，需要包括 [Windows 调试工具](https://msdn.microsoft.com/Library/Windows/Hardware/Ff551063)。

WDK 使用 MSBuild.exe，Visual Studio 用户界面中提供有此程序，并且它也可以作为命令行工具提供。 在 Visual Studio 环境中创建的驱动程序使用项目和解决方案文件来描述项目或项目组。 Visual Studio 环境提供有用于将旧源和目录文件转换成项目和解决方案文件的工具。

Visual Studio 环境提供适用于以下项的模板：

-   新驱动程序
-   驱动程序包
-   新测试
-   现有测试的增强功能
-   自定义驱动程序部署脚本

在 Visual Studio 环境中，你可以配置构建流程，使其自动创建和签署驱动程序包。 Visual Studio 中提供了静态和实时分析工具。 你可以配置用于测试驱动程序的目标计算机，并在每次重建时将你的驱动程序自动部署到目标计算机。 在 Visual Studio 中，你可以与目标计算机建立内核模式调试会话。 你可以从多个运行时测试中进行选择，也可以编写自己的测试。

本部分的主题介绍了如何使用 Visual Studio 执行驱动程序开发、部署和测试中涉及的各任务。




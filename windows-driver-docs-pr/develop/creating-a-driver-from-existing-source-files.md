---
ms.assetid: C5CD87E3-26C0-48AA-B75E-1EFFB0B5519D
title: 从现有源文件创建驱动程序
description: WDK 已与 Microsoft Visual Studio 集成，并使用与你用于生成 Visual Studio 解决方案和项目的相同编译器和生成工具。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f55796770618dede44903f069cecd5822195864
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734459"
---
# <a name="creating-a-driver-from-existing-source-files"></a>从现有源文件创建驱动程序

WDK 已与 Microsoft Visual Studio 集成，并使用与你用于生成 Visual Studio 解决方案和项目的相同编译器和生成工具。 [MSBuild](/visualstudio/msbuild/msbuild) 替换了 Windows 驱动程序工具包 (WDK) 8 以前的 WDK 版本中使用的 Windows 生成实用工具 (Build.exe)。

若要转换使用以前版本的 WDK 创建的驱动程序，请使用一个提供的 Windows 驱动程序模板在 Visual Studio 中创建新的 Windows 驱动程序解决方案。 如果你从驱动程序模型的模板开始，项目的结构将是现成的，并将选择正确的平台工具集。 然后，你可以将源文件添加到解决方案。 有关选择模板的信息，请参阅[创建新的设备功能驱动程序](creating-a-new-driver.md)、[创建新的筛选器驱动程序](creating-a-new-filter-driver.md)或[创建新的软件驱动程序](creating-a-new-software-driver.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [WDK 和 Visual Studio 生成环境](../devtest/wdk-and-visual-studio-build-environment.md)
* [ProjectUpgradeTool](../devtest/projectupgradetool.md)
* [MSBuild](/visualstudio/msbuild/msbuild)
* [演练：使用 MSBuild](/visualstudio/msbuild/walkthrough-using-msbuild)
* [创建新的设备功能驱动程序](creating-a-new-driver.md)
* [创建新的筛选器驱动程序](creating-a-new-filter-driver.md)
* [创建新的软件驱动程序](creating-a-new-software-driver.md)

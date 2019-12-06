---
title: 提供 INF 文件
description: 提供 INF 文件
ms.assetid: 208726d9-6f62-46a4-84a1-6fab3895bbe3
keywords:
- 驱动程序包 WDK、INF 文件
- 包 WDK、INF 文件
- INF 文件 WDK，关于 INF 文件
- 信息文件 WDK
- .inf 文件
- 设备安装 WDK、INF 文件
- 安装设备 WDK、INF 文件
- 设备安装 WDK、INF 文件
- INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a7f33c3a70b7f75847ab02a0031d5bd123c26c7
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862974"
---
# <a name="supplying-an-inf-file"></a>提供 INF 文件





每个驱动程序包都必须包含一个 INF 文件，[设备安装组件](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))在安装设备时将读取该文件。 INF 文件不是安装脚本。 它是一个 ASCII 或 Unicode 文本文件，它提供设备和驱动程序的信息，包括驱动程序文件、注册表项、设备 Id、[目录文件](catalog-files.md)以及安装设备或驱动程序所需的版本信息。 INF 不仅在第一次安装设备或驱动程序时使用，还在用户通过设备管理器请求驱动程序更新时使用。

INF 文件的确切内容和格式取决于[设备安装程序类](device-setup-classes.md)。 [Inf 部分摘要](summary-of-inf-sections.md)介绍了每种类型的 INF 中所需的信息。 通常，每个制造商的信息位于[**INF*模型*部分**](inf-models-section.md)。 "**模型**" 部分中的条目引用包含特定于模型的详细信息的[**INF *DDInstall*部分**](inf-ddinstall-section.md)。

Microsoft Windows 驱动程序工具包（WDK）的 *\\工具*目录中提供的[InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)工具将检查所有跨类 INF 节和指令的语法和结构，以及除打印机之外的所有安装程序类的类特定扩展。

从 Windows 2000 开始，你可以使用单个 INF 文件在所有版本的 Windows 操作系统上安装。 有关详细信息，请参阅[为多个平台和操作系统创建 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。 如果你的设备将出售到国际市场，你应[创建一个国际 INF 文件](creating-international-inf-files.md)。 根据所涉及的位置，国际 INF 文件可能必须是 Unicode 文件而不是 ASCII。

为驱动程序创建 INF 文件的一个好方法是修改 WDK 提供的示例之一。 大多数 WDK 示例驱动程序都包含与示例驱动程序相同的目录中的 INF 文件。

有关 INF 文件的详细信息，请参阅[创建 Inf 文件](overview-of-inf-files.md)、 [InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)的文档、WDK 中的设备特定文档，以及与你的设备类似的设备的示例驱动程序提供的 INF 文件。

 

 






---
title: 生成和加载 WDF 驱动程序
description: 本主题介绍如何在 Visual Studio 中选择目标操作系统和驱动程序项目的 framework 版本。 它还介绍了共同安装程序以及如何确定是否应驱动程序包中包括此组件。
ms.assetid: 82c77b1f-4bf0-46d9-bae3-822e9be5a7fb
keywords:
- 内核模式驱动程序 WDK KMDF，构建驱动程序
- KMDF WDK，构建驱动程序
- 内核模式驱动程序框架 WDK 构建驱动程序
- 内核模式驱动程序 WDK KMDF，加载驱动程序
- KMDF WDK、 加载驱动程序
- 内核模式驱动程序框架 WDK、 加载驱动程序
- 构建驱动程序 WDK、 KMDF
- 加载驱动程序 WDK KMDF
- 生成实用工具 WDK、 KMDF
- KMDF 驱动程序 WDK KMDF，构建
- KMDF 驱动程序 WDK KMDF，加载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d70338ba8c3834b803fad13de109cea49061ca98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362707"
---
# <a name="building-and-loading-a-wdf-driver"></a>生成和加载 WDF 驱动程序


本主题介绍如何在 Visual Studio 中选择目标操作系统和驱动程序项目的 framework 版本。 它还介绍了共同安装程序以及如何确定是否应驱动程序包中包括此组件。

## <a name="which-framework-version-should-i-use"></a>应使用哪个框架版本？


如果您的驱动程序需要仅在 Windows 8.1 上运行，请使用内核模式驱动程序框架 (KMDF) 版本 1.13 或用户模式驱动程序框架 (UMDF) 2.0 版。

如果您的驱动程序必须在操作系统中工作，早于 Windows 8.1，我们建议你使用 KMDF 或 UMDF 版本 1.11。

可以使用 Windows Driver Kit (WDK) 随 Windows 8.1 为生成 KMDF 1.9、 1.11，和 1.13 驱动程序，以及 UMDF 1.9 1.11，和 2.0 的驱动程序。

## <a name="how-do-i-set-the-versions-in-visual-studio"></a>如何将版本设置 Visual Studio 中？


如果您正在构建的最新版本的 Windows 和最新 KMDF 或 UMDF 版本的驱动程序项目，可以保留默认值，并跳过此步骤。

否则，请执行以下步骤：

-   更改**项目配置**中设置**Configuration Manager**为适当的值 (如**Win7 调试**)。
-   更改 KMDF\_版本\_一些服务障碍或 UMDF\_版本\_中的次要值[驱动程序模型设置](https://msdn.microsoft.com/windows-drivers/develop/driver_model_settings_properties_for_driver_projects)为适当的值 （如 11)。

有关 KMDF 和 UMDF 版本的详细信息，请参阅[KMDF 版本历史记录](kmdf-version-history.md)并[UMDF 版本历史记录](umdf-version-history.md)。

## <a name="when-do-i-need-to-include-a-co-installer-or-msu-in-my-driver-package"></a>何时需要我的驱动程序包中包括的共同安装程序或.msu？


如果生成了驱动程序的 Windows 8.1 使用 KMDF 1.13 或 UMDF 2.0，您不需要在 INF 文件中包含共同安装程序、 自定义安装程序或引用。

如果您的驱动程序必须在操作系统中工作，早于 Windows 8.1，我们建议你使用 KMDF 或 UMDF 版本 1.11 和驱动程序包中包括 Microsoft 提供 framework 更新。

Framework 更新，使其可以运行使用更高版本的 framework 版本而不是包含在操作系统构建的驱动程序。 例如，在 Windows 8 中包含 KMDF 1.11。 但可以在 Windows Vista 或 Windows 7 上运行一个 KMDF 1.11 的驱动程序。 您可以执行此操作之前，但是，您必须确保 KMDF 1.11 框架库取代了早期版本的操作系统中包括的框架库 (在这种情况下，KMDF 1.7 和 KMDF 1.9 分别)。 执行此操作的重新分发的 Microsoft 提供共同安装程序或.msu 文件与驱动程序包。

## <a name="linking-and-loading"></a>链接和加载


在驱动程序添加到合适的框架库、 库的加载程序和存根 （stub） 文件生成 Microsoft Visual Studio，MSBuild 链接中的 Windows 驱动程序框架 (WDF) 项目时，在 WDK 中包含所有这些。 (库和加载程序还包含在框架的[共同安装程序](installing-the-framework-s-co-installer.md)以便如有必要，可以将其分发与驱动程序包。)

存根 （stub） 文件包含一个特殊的入口点例程：**FxDriverEntry**。 MSBuild 设置存根 （stub） 的**FxDriverEntry**例程作为基于框架的驱动程序的初始入口点。

当操作系统加载基于 framework 的驱动程序时，它还会加载存根 （stub） 文件和库的加载程序。 接下来，系统将调用存根 （stub） 文件**FxDriverEntry**例程。 然后，此例程调用加载程序。 加载程序将确定框架库，该驱动程序要求，然后加载正确的版本[版本的库](framework-library-versioning.md)作为内核模式服务 （如果尚未加载）。 最后，库调用的驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)例程。

 

 






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
ms.date: 05/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 73b5cb4a3e48a09a617980e4c81f23b0ef20682e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359126"
---
# <a name="building-and-loading-a-wdf-driver"></a>生成和加载 WDF 驱动程序


本主题介绍如何在 Visual Studio 中选择目标操作系统和驱动程序项目的 framework 版本。

若要确定是否需要的驱动程序包中包含可再发行框架组件，请参阅[可再发行框架组件](installation-components-for-kmdf-drivers.md)。


## <a name="which-framework-version-should-i-use"></a>应使用哪个框架版本？

*   若要针对 Windows XP，请使用 WDF 1.9 或更早版本。
*   若要针对 Windows Vista、 Windows 7 或 Windows 8，使用 WDF 1.11 或更早版本。
*   到目标 Windows 8.1 中，使用 1.13 或更早版本，KMDF 或 UMDF 1.x 中或 UMDF 2.0。
*   到目标 Windows 10 版本 1507年、 使用 1.15 或更早版本，KMDF 或 UMDF 1.x 中或 UMDF 2.15 或更早版本。

有关 KMDF 和 UMDF 版本的详细信息，请参阅[KMDF 版本历史记录](kmdf-version-history.md)并[UMDF 版本历史记录](umdf-version-history.md)。

* [KMDF 版本历史记录](kmdf-version-history.md)
* [UMDF 版本历史记录](umdf-version-history.md)

## <a name="how-do-i-set-the-versions-in-visual-studio"></a>如何将版本设置 Visual Studio 中？


如果您正在构建的最新版本的 Windows 和最新 KMDF 或 UMDF 版本的驱动程序项目，可以保留默认值，并跳过此步骤。

否则，请执行以下步骤：

-   右键单击解决方案并选择**Configuration Manager**。  设置**项目配置**到所需的值 (例如**调试**)。
-   右键单击驱动程序项目，然后选择**属性**。  打开**配置属性-> 驱动程序设置-> 驱动程序模型**。  更改**KMDF 版本次要 （目标版本）** 或**UMDF 版本次要 （目标版本）** 中的值[驱动程序模型设置](../develop/driver-model-settings-properties-for-driver-projects.md)到所需的值。  有关信息**KMDF 版本次要 （最低要求）** 并**UMDF 版本次要 （最低要求）** ，请参阅[指定最小所需](https://docs.microsoft.com/windows-hardware/drivers/wdf/building-a-wdf-driver-for-multiple-versions-of-windows#specifying-minimum-required)。

可以使用 Windows Driver Kit (WDK) 随 Windows 10 构建 KMDF 1.9 1.29 驱动程序，以及 UMDF 1.9 2.29 驱动程序。

有关 KMDF 和 UMDF 版本的详细信息，请参阅[KMDF 版本历史记录](kmdf-version-history.md)并[UMDF 版本历史记录](umdf-version-history.md)。

* [KMDF 版本历史记录](kmdf-version-history.md)
* [UMDF 版本历史记录](umdf-version-history.md)

## <a name="linking-and-loading"></a>链接和加载


在驱动程序添加到合适的框架库、 库的加载程序和存根 （stub） 文件生成 Microsoft Visual Studio，MSBuild 链接中的 Windows 驱动程序框架 (WDF) 项目时，在 WDK 中包含所有这些。 (库和加载程序还包含在框架的[共同安装程序](installing-the-framework-s-co-installer.md)以便如有必要，可以将其分发与驱动程序包。)

存根 （stub） 文件包含一个特殊的入口点例程：**FxDriverEntry**。 MSBuild 设置存根 （stub） 的**FxDriverEntry**例程作为基于框架的驱动程序的初始入口点。

当操作系统加载基于 framework 的驱动程序时，它还会加载存根 （stub） 文件和库的加载程序。 接下来，系统将调用存根 （stub） 文件**FxDriverEntry**例程。 然后，此例程调用加载程序。 加载程序将确定框架库，该驱动程序要求，然后加载正确的版本[版本的库](framework-library-versioning.md)作为内核模式服务 （如果尚未加载）。 最后，库调用的驱动程序[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)例程。


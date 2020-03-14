---
title: 生成和加载 WDF 驱动程序
description: 本主题介绍如何在 Visual Studio 中为驱动程序项目选择目标操作系统和 framework 版本。 它还介绍了共同安装程序，以及如何确定是否应在驱动程序包中包含此组件。
ms.assetid: 82c77b1f-4bf0-46d9-bae3-822e9be5a7fb
keywords:
- 内核模式驱动程序 WDK KMDF，构建驱动程序
- KMDF WDK，构建驱动程序
- 内核模式驱动程序框架 WDK，构建驱动程序
- 内核模式驱动程序 WDK KMDF，加载驱动程序
- KMDF WDK，加载驱动程序
- 内核模式驱动程序框架 WDK，加载驱动程序
- 构建驱动程序 WDK，KMDF
- 加载驱动程序 WDK KMDF
- 生成实用工具 WDK，KMDF
- KMDF 驱动程序 WDK KMDF，大楼
- KMDF 驱动程序 WDK KMDF，加载
ms.date: 05/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 73b5cb4a3e48a09a617980e4c81f23b0ef20682e
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242930"
---
# <a name="building-and-loading-a-wdf-driver"></a>生成和加载 WDF 驱动程序


本主题介绍如何在 Visual Studio 中为驱动程序项目选择目标操作系统和 framework 版本。

若要确定是否需要在驱动程序包中包含可再发行的框架组件，请参阅可[再发行框架组件](installation-components-for-kmdf-drivers.md)。


## <a name="which-framework-version-should-i-use"></a>我应该使用哪个 framework 版本？

*   若要面向 Windows XP，请使用 WDF 1.9 或更早版本。
*   若要面向 Windows Vista、Windows 7 或 Windows 8，请使用 WDF 1.11 或更早版本。
*   若要以 Windows 8.1 为目标，请使用 KMDF 1.13 或更低版本，或者使用 UMDF 1.x 或 UMDF 2.0。
*   若要面向 Windows 10 版本1507，请使用 KMDF 1.15 或更低版本，或者使用 UMDF 1.x 或 UMDF 2.15 或更早版本。

有关 KMDF 和 UMDF 版本的详细信息，请参阅[KMDF 版本历史记录](kmdf-version-history.md)和[Umdf 版本历史记录](umdf-version-history.md)。

* [KMDF 版本历史记录](kmdf-version-history.md)
* [UMDF 版本历史记录](umdf-version-history.md)

## <a name="how-do-i-set-the-versions-in-visual-studio"></a>如何实现在 Visual Studio 中设置版本吗？


如果要为 Windows 的最新版本和最新的 KMDF 或 UMDF 版本构建驱动程序项目，可以保留默认值并跳过此步骤。

否则，请执行以下步骤：

-   右键单击该解决方案，然后选择 " **Configuration Manager**"。  将**项目配置**设置为所需的值（例如 "**调试**"）。
-   右键单击驱动程序项目，然后选择 "**属性**"。  打开**配置属性-> 驱动程序设置-> 驱动程序模型**。  将[驱动程序模型设置](../develop/driver-model-settings-properties-for-driver-projects.md)中的**KMDF 版本次要（目标版本）** 或**UMDF 版本次要（目标版本）** 值更改为所需的值。  有关**KMDF 版本（必需）** 和**UMDF 版本（最低**要求）的信息，请参阅[指定所需的最小](https://docs.microsoft.com/windows-hardware/drivers/wdf/building-a-wdf-driver-for-multiple-versions-of-windows#specifying-minimum-required)值。

你可以使用 Windows 10 随附的 Windows 驱动程序工具包（WDK）来构建 KMDF 1.9-1.29 驱动程序，并提供 UMDF 1.9-2.29 驱动程序。

有关 KMDF 和 UMDF 版本的详细信息，请参阅[KMDF 版本历史记录](kmdf-version-history.md)和[Umdf 版本历史记录](umdf-version-history.md)。

* [KMDF 版本历史记录](kmdf-version-history.md)
* [UMDF 版本历史记录](umdf-version-history.md)

## <a name="linking-and-loading"></a>链接和加载


当你在 Microsoft Visual Studio 中生成 Windows 驱动程序框架（WDF）项目时，MSBuild 会将你的驱动程序链接到相应的框架库、库的加载程序和一个存根文件，这一切都包含在 WDK 中。 （库和加载程序也包含在框架的[共同安装程序](installing-the-framework-s-co-installer.md)中，因此，如有必要，你可以将其与驱动程序包一起分发。）

存根文件包含一个特殊的入口点例程： **FxDriverEntry**。 MSBuild 将存根的**FxDriverEntry**例程设置为基于框架的驱动程序的初始入口点。

当操作系统加载基于框架的驱动程序时，它还会加载存根文件和库的加载程序。 接下来，系统调用存根文件的**FxDriverEntry**例程。 然后，此例程调用加载程序。 加载程序将确定驱动程序所需的框架库版本，然后将正确版本的[库](framework-library-versioning.md)作为内核模式服务（如果尚未加载）加载。 最后，库调用驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)例程。


---
title: 可再发行框架组件
description: 本主题介绍作为一部分的 Windows 8.1 的 Windows Driver Kit (WDK) 以及如何确定要添加到驱动程序包包含 Microsoft 提供的可再发行组件 framework 更新。
ms.assetid: 63fbe66e-fa1b-4a70-a8ea-df4f3df9bad4
keywords:
- 基于框架的驱动程序 WDK KMDF，安装
- 有关安装 KMDF 驱动程序的 INF 文件 WDK KMDF
- WDK KMDF 驱动程序的安装组件
ms.date: 05/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3e68121fbed77beac9066701bafc6bfb54920a56
ms.sourcegitcommit: 7bd9480d40021827e6d46f9b83638dac85380e88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2019
ms.locfileid: "65875100"
---
# <a name="redistributable-framework-components"></a>可再发行框架组件

本主题介绍作为一部分的 Windows Driver Kit (WDK) 中，以及如何确定要添加到驱动程序包包含 Microsoft 提供的可再发行组件 framework 更新。

可再发行框架更新，使其可以运行使用更高版本的 framework 版本而不是包含在操作系统构建的驱动程序。 例如，在 Windows 8 中包含 KMDF 1.11。 但可以在 Windows Vista 或 Windows 7 上运行一个 KMDF 1.11 的驱动程序。 您可以执行此操作之前，但是，您必须确保 KMDF 1.11 框架库取代了早期版本的操作系统中包括的框架库 (在这种情况下，KMDF 1.7 和 KMDF 1.9 分别)。 执行此操作的重新分发的 Microsoft 提供共同安装程序或.msu 文件与驱动程序包。

## <a name="when-do-i-need-to-include-a-co-installer-or-msu-in-my-driver-package"></a>何时需要我的驱动程序包中包括的共同安装程序或.msu？

首先，确定您的驱动程序将支持的 Windows 版本。  此基础，确定[要使用的框架版本](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)。

如果所选的 WDF 版本晚于与目标操作系统一起提供的版本，包括驱动程序包中的辅助安装程序或.msu 文件。

例如，您希望您的驱动程序在 Windows 7 上运行。  您可以选择生成您使用 WDF 1.9 或 WDF 1.11 的驱动程序。 如果您选择 1.9，提供与 Windows 7，则无需更新系统。 但是，如果您选择 1.11，您需要包括您的驱动程序与 WDF 1.11 更新包。

## <a name="should-i-include-the-co-installer-or-the-msu-file"></a>应包含共同安装程序或.msu 文件？

如果驱动程序安装时触发插入新的硬件设备的系统，要安装只有驱动程序，包括驱动程序包中共同安装程序。 然后，引用在 INF 文件中，辅助安装程序中所述[INF 文件中指定 KMDF 共同安装程序](installing-the-framework-s-co-installer.md)。

如果你需要安装除了您的驱动程序的应用程序，则应改为重新分发以及调用它的安装程序应用程序的相关 MSU 包 (例如 kmdf-1.11-Win.6.0.msu)。
在这种情况下，需要无 INF 项。

您不再需要辅助安装程序和.msu 文件。


## <a name="where-can-i-find-these-files-and-whats-included"></a>在哪里可以找到这些文件，并包含的内容？

共同安装程序位于`%program files%\Windows Kits\<version>\redist\wdf`。

此目录包含以下文件，对于 x86 和 x64:

-   *WdfCoinstaller01007.dll*， *WdfCoinstaller01009.dll*， *WdfCoinstaller01011.dll* （对于 KMDF 1.7/1.9/1.11 共同安装程序）。
-   *WUDFUpdate\_01007.dll*， *WUDFUpdate\_01009.dll*， *WUDFUpdate\_01011.dll* （对于 UMDF 共同安装程序）。
-   *winusbcoinstaller.dll*， *winusbcoinstaller2.dll* （共同安装程序为 WinUSB 1.5/1.9 中）。

如果想要的 MSU 文件，请下载并安装程序包 （在 MSI 格式），从[WDK 8 可再发行组件](https://go.microsoft.com/fwlink/p/?LinkID=253170)。
安装完成后，MSU 和共同安装程序可在`%program files%\Windows Kits\8.0\redist\wdf`。

## <a name="co-installer-naming-and-versioning"></a>命名的共同安装程序和版本控制

名为共同安装程序**WdfCoInstaller**<em>MMmmm</em>**.dll**。

-   *MM*是主版本号。
-   *mmm*是次版本号。

例如，对于 1.0 版的辅助安装程序的文件名是*WdfCoInstaller01000.dll*，并且版本 1.11 的文件名*WdfCoInstaller01011.dll*。

包含与驱动程序包的共同安装程序的版本必须与用于开发您的驱动程序的框架库的版本匹配。

请注意框架库的文件的名称，包括仅主版本号。 有关库文件名称的详细信息，请参阅[Framework 库版本控制](framework-library-versioning.md)。

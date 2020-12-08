---
title: 可再发行框架组件
description: 本主题介绍了 Microsoft 提供的可再发行框架更新，这些更新作为 Windows 驱动程序工具包的一部分包含在 Windows 8.1 (WDK) ，以及如何确定要添加到驱动程序包中的文件。
keywords:
- 基于框架的驱动程序 WDK KMDF，安装
- INF 文件 WDK KMDF，关于安装 KMDF 驱动程序
- 驱动程序的安装组件 WDK KMDF
ms.date: 05/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: a4801251c6b6b5e95af341b1082fca249bfc5a1c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837607"
---
# <a name="redistributable-framework-components"></a>可再发行框架组件

本主题介绍了 Microsoft 提供的可再发行框架更新，这些更新作为 Windows 驱动程序工具包的一部分包含 (WDK) ，以及如何确定要添加到驱动程序包。

可再发行框架更新使你可以运行使用比操作系统中包含的版本更高的版本生成的驱动程序。 例如，KMDF 1.11 包含在 Windows 8 中。 但你可以在 Windows Vista 或 Windows 7 上运行 KMDF 1.11 驱动程序。 但是，在执行此操作之前，必须确保 KMDF 1.11 framework 库替换了之前操作系统中包含的框架库 (在此示例中，分别) KMDF 1.7 和 KMDF 1.9。 为此，可将 Microsoft 提供的共同安装程序或 .msu 文件重新分发到驱动程序包。

## <a name="when-do-i-need-to-include-a-co-installer-or-msu-in-my-driver-package"></a>何时需要在驱动程序包中包含共同安装程序或 .msu？

首先，确定驱动程序将支持的 Windows 版本。  基于这一点，确定 [要使用的 framework 版本](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)。

如果所选 WDF 版本比目标 OS 附带的版本新，请在驱动程序包中包含共同安装程序或 .msu 文件。

例如，你希望你的驱动程序在 Windows 7 上运行。  可以选择使用 WDF 1.11 或 WDF 1.9 生成驱动程序。 如果选择了 "1.9" （随 Windows 7 一起提供），则无需更新系统。 另一方面，如果你选择1.11，则需要在你的驱动程序中包含 WDF 1.11 更新包。

## <a name="should-i-include-the-co-installer-or-the-msu-file"></a>是否应包括共同安装程序或 .msu 文件？

如果通过将新的硬件设备插入系统并仅安装驱动程序来触发驱动程序安装，请在驱动程序包中包含共同安装程序。 然后在 INF 文件中引用共同安装程序，如在 [Inf 文件中指定 KMDF 共同安装程序](installing-the-framework-s-co-installer.md)中所述。

如果除驱动程序外，还需要安装一个应用程序，则应改为重新发布相关的 MSU 包 (例如 kmdf-1.11-Win) 连同调用它的安装程序。
在这种情况下，不需要任何 INF 条目。

你永远都不需要共同安装程序和 .msu 文件。


## <a name="where-can-i-find-these-files-and-whats-included"></a>在哪里可以找到这些文件，包括哪些内容？

共同安装程序位于 `%program files%\Windows Kits\<version>\redist\wdf` 。

此目录包含适用于 x86 和 x64 的以下文件：

-   *WdfCoinstaller01007.dll*， *WdfCoinstaller01009.dll*， *WdfCoinstaller01011.dll* (KMDF 1.7/1.9/1.11) 的共同安装程序。
-   *WUDFUpdate \_01007.dll*、 *WUDFUpdate \_01009.dll*、 *WUDFUpdate \_01011.dll* (用于 UMDF) 的共同安装程序。
-   *winusbcoinstaller.dll*， *winusbcoinstaller2.dll* (WinUSB 1.5/1.9) 的共同安装程序。

如果需要 MSU 文件，请从 [WDK 8 可再发行组件](https://go.microsoft.com/fwlink/p/?LinkID=253170)) 下载并安装 MSI 格式的程序包 (。
安装后，可以在中找到 MSU 和共同安装程序 `%program files%\Windows Kits\8.0\redist\wdf` 。

## <a name="co-installer-naming-and-versioning"></a>共同安装程序命名和版本控制

共同安装程序的名称为 **WdfCoInstaller**<em>嗯</em>**。**

-   *MM* 是主要版本号。
-   *mmm* 为次版本号。

例如， *WdfCoInstaller01000.dll* 版本1.0 的文件的文件名，并且 *WdfCoInstaller01011.dll* 版本1.11 的文件名。

驱动程序包中包含的共同安装程序的版本必须与用于开发驱动程序的 framework 库的版本匹配。

请注意，框架库的文件名只包含主要版本号。 有关库文件名的详细信息，请参阅 [框架库版本控制](framework-library-versioning.md)。

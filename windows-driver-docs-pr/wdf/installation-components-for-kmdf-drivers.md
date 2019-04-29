---
title: 可再发行框架组件
description: 本主题介绍作为一部分的 Windows 8.1 的 Windows Driver Kit (WDK) 以及如何确定要添加到驱动程序包包含 Microsoft 提供的可再发行组件 framework 更新。
ms.assetid: 63fbe66e-fa1b-4a70-a8ea-df4f3df9bad4
keywords:
- 基于框架的驱动程序 WDK KMDF，安装
- 有关安装 KMDF 驱动程序的 INF 文件 WDK KMDF
- WDK KMDF 驱动程序的安装组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73a7404106beb9881c7764c25c3fe4f24bc782be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378171"
---
# <a name="redistributable-framework-components"></a>可再发行框架组件


本主题介绍作为一部分的 Windows 8.1 的 Windows Driver Kit (WDK) 以及如何确定要添加到驱动程序包包含 Microsoft 提供的可再发行组件 framework 更新。

若要确定是否需要在所有驱动程序包中包括任何 framework 更新，请参阅[构建和 WDF 驱动程序加载](building-and-loading-a-kmdf-driver.md)。 如果不这样做，请跳过本主题。

## <a name="should-i-include-the-co-installer-or-the-msu-file"></a>应包含共同安装程序或.msu 文件？


如果驱动程序安装时触发插入新的硬件设备的系统，要安装只有驱动程序，包括驱动程序包中共同安装程序。 然后，引用在 INF 文件中，辅助安装程序中所述[INF 文件中指定 KMDF 共同安装程序](installing-the-framework-s-co-installer.md)。

如果你需要安装除了您的驱动程序的应用程序，则应改为重新分发以及调用它的安装程序应用程序的相关 MSU 包 (例如 kmdf-1.11-Win.6.0.msu)。 您可以在 WDK 中的 src 中找到此类应用程序的示例\\常规\\installwdf 目录。

在后一种情况，不需要其他任何 INF 条目。

## <a name="where-can-i-find-these-files-and-whats-included"></a>在哪里可以找到这些文件，并包含的内容？


生成您在 Visual Studio 中的驱动程序时，MSBuild 将生成的程序包目录，以及驱动程序的辅助安装程序。*sys*和 INF 文件。

可再发行框架更新文件的完整集是否位于 *%programfiles%*\\windows 工具包\\*&lt;WDK 版本&gt;* \\redist\\wdf。

此目录包含以下文件，对于 x86 和 x64:

-   *WdfCoinstaller01009.dll*， *wdfcoinstaller01011.dll* （共同安装程序 KMDF 1.9/1.11）。
-   *WUDFUpdate\_01009.dll*， *WUDFUpdate\_01011.dll* （对于 UMDF 共同安装程序）。
-   *winusbcoinstaller.dll*， *winusbcoinstaller2.dll* （共同安装程序为 WinUSB 1.5/1.9 中）。
-   *WinUSB\_1.9.msu* – WinUSB 1.9 版更新，也可用作[KB971286](http://support.microsoft.com/kb/971286)。
-   *kmdf 1.11 Win 6.0.msu*， *kmdf 1.11 Win 6.1.msu* -KMDF 1.11 适用于 Windows Vista （6.0 版） 的 Windows 更新包 / Windows 7 (v6.1)。
-   *umdf 1.11 Win 6.0.msu*， *umdf 1.11 Win 6.1.msu* – UMDF 1.11 适用于 Windows Vista （6.0 版） 的 Windows 更新包 / Windows 7 (v6.1)。

## <a name="co-installer-naming-and-versioning"></a>命名的共同安装程序和版本控制


名为共同安装程序**WdfCoInstaller**<em>MMmmm</em>**.dll**。

-   *MM*是主版本号。
-   *mmm*是次版本号。

例如，对于 1.0 版的辅助安装程序的文件名是*WdfCoInstaller01000.dll*，并且版本 1.11 的文件名*WdfCoInstaller01011.dll*。

包含与驱动程序包的共同安装程序的版本必须与用于开发您的驱动程序的框架库的版本匹配。

请注意框架库的文件的名称，包括仅主版本号。 有关库文件名称的详细信息，请参阅[Framework 库版本控制](framework-library-versioning.md)。

 

 






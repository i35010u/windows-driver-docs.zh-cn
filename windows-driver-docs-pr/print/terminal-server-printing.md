---
title: 终端服务器打印
description: 终端服务器打印
ms.assetid: 627d05f6-1499-4645-ad9a-b1a09f41b0c9
keywords:
- 打印机驱动程序 WDK，终端服务器
- 打印 WDK 的终端服务器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 533e945e07f8fcdc22eb6d8a5dbed996b69d61a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388059"
---
# <a name="terminal-server-printing"></a>终端服务器打印





Microsoft Windows 2000 和更高版本支持终端服务技术，它允许多个用户连接到单个服务器系统。 此服务器被称为终端服务器。 有关终端服务的详细讨论，请参阅 Windows SDK 文档。

如果你正在开发的打印机微型驱动程序或驱动程序适用于 Windows 2000 或更高版本，您无需执行任何特殊操作来支持连接到终端服务器的打印机。 但是，必须按照指定 Windows Driver Kit (WDK) 中的所有设计、 实现和安装指南。 具体而言，必须使用以下规则：

-   如果可能，只需提供适用于 Microsoft 提供的以下驱动因素之一的微型驱动程序支持您的打印机：

    [Microsoft XPS 打印机驱动程序](xpsdrv-printer-driver.md)

    [Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)

    [Microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md)

    [Microsoft 绘图仪驱动程序](microsoft-plotter-driver.md)

-   在 Windows Vista 中，您必须设计打印机图形 DLL 来在用户模式下执行。 请参阅[选择用户模式或内核模式](choosing-user-mode-or-kernel-mode.md)。

-   如果你的设备必须支持的自定义驱动程序，您的驱动程序必须遵循与 Microsoft 的完全[打印机驱动程序体系结构](printer-driver-architecture.md)。 特别是：
    1.  必须创建[打印机接口 DLL](printer-interface-dll.md)。
    2.  必须创建[打印机图形 DLL](printer-graphics-dll.md)。 此 DLL 可以在用户模式或内核模式下执行，但用户模式是首选。
    3.  如果创建内核模式代码时，必须测试的代码使用[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)。
    4.  你必须提供安装程序 INF 文件的基础的安装过程中所述[安装和配置打印机驱动程序](installing-and-configuring-printer-drivers.md)。

所有自定义驱动程序代码必须是可重入。 用户模式代码应使用关键节对象 （Windows SDK 文档中所述）。 内核模式代码应使用信号量 (请参阅[ **EngCreateSemaphore** ](https://msdn.microsoft.com/library/windows/hardware/ff564760)和相关函数)。

打印机驱动程序和自定义后台处理程序组件必须访问注册表仅通过接口提供专用于这些驱动程序和后台处理程序组件，WDK 的相应部分中所述。

### <a name="installation-considerations"></a>安装注意事项

通常情况下，您需要做为安装提供当用户调用时，Microsoft 的打印机类安装程序可以读取的 INF 文件**添加打印机**向导。 有时，还需要自定义安装程序代码 （共同安装程序或类安装程序）。 如果必须创建自定义安装程序代码，请记住以下：

-   用户或安装程序代码必须将终端服务器置于安装模式。 （有关详细信息，请参阅 Microsoft Windows SDK 文档）。

-   不要尝试替换系统文件。 Windows 文件保护禁止替换系统文件。

-   避免需要尽可能多的系统重新启动。 使用以下指南：
    1.  不会替代未发生更改的驱动程序文件。 例如，如果已安装最新版本，则应不更新由多个设备共享的文件。
    2.  如果必须替换的文件时，安装程序代码应采取措施来卸载旧版本，然后加载新版本 （例如，通过停止该驱动程序服务，并替换文件，然后重新启动服务）。
    3.  要求用户先注销，然后重新记录，要优于需重启系统。

有关共同安装程序和类安装程序的详细信息，请参阅[编写类安装程序和共同安装程序](https://msdn.microsoft.com/library/windows/hardware/ff819060)。

**请注意**  之前编写自定义安装程序代码时，务必要读取终端服务编程的 Windows SDK 文档中提供的指导原则。

 

### <a name="user-interface-considerations"></a>用户界面的注意事项

由用户运行的自定义安装程序代码可以显示用户界面。

几乎所有打印机驱动程序代码在后台处理程序的执行上下文中运行，因此不能显示用户界面。 可以显示用户界面，仅可被打印机接口的 Dll，并且只能从以下函数：

-   [ **DrvDevicePropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff548542)并[ **DrvDocumentPropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff548548)函数，创建属性页。

-   [ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)函数，用于接收标识打印机事件的事件代码。 请注意，该函数可以仅为打印机显示用户界面\_事件\_添加\_连接和打印机\_事件\_删除\_连接事件代码。

在后台处理程序的上下文中执行所有其他打印机驱动程序代码。 此上下文中调用**MessageBox**或**MessageBoxEx**允许，但您必须设置 MB\_服务\_通知。 这些函数是 Windows SDK 文档中所述。

 

 





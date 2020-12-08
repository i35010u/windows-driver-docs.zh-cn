---
title: 终端服务器打印
description: 终端服务器打印
keywords:
- 打印机驱动程序 WDK，终端服务器
- 终端服务器打印 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd9d38e84aee04acbb49f82a7c401b8f4b05e196
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806723"
---
# <a name="terminal-server-printing"></a>终端服务器打印





Microsoft Windows 2000 和更高版本支持终端服务，这是允许多个用户连接到单个服务器系统的一种技术。 此服务器系统称为终端服务器。 有关终端服务的详细讨论，请参阅 Windows SDK 文档。

如果要开发适用于 Windows 2000 或更高版本的打印机微型驱动程序或驱动程序，则无需执行任何特殊操作即可支持连接到终端服务器的打印机。 但是，必须遵循 Windows 驱动程序工具包 (WDK) 中指定的所有设计、实施和安装指南。 具体来说，您必须使用以下规则：

-   如果可能，只需提供适用于以下 Microsoft 提供的驱动程序之一的微型驱动程序，即可支持打印机：

    [Microsoft XPS 打印机驱动程序](xpsdrv-printer-driver.md)

    [Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)

    [Microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md)

    [Microsoft 绘图仪驱动程序](microsoft-plotter-driver.md)

-   在 Windows Vista 中，必须设计要在用户模式下执行的打印机图形 DLL。 请参阅 [选择用户模式或内核模式](choosing-user-mode-or-kernel-mode.md)。

-   如果自定义驱动程序必须支持您的设备，则您的驱动程序必须完全符合 Microsoft 的 [打印机驱动程序体系结构](printer-driver-architecture.md)。 具体而言：
    1.  您必须创建一个 [打印机接口 DLL](printer-interface-dll.md)。
    2.  必须创建 [打印机图形 DLL](printer-graphics-dll.md)。 此 DLL 可以在用户模式或内核模式下执行，但首选用户模式。
    3.  如果创建内核模式代码，则必须使用 [驱动程序验证程序](../devtest/driver-verifier.md)来测试代码。
    4.  必须按照安装 [和配置打印机驱动程序](installing-and-configuring-printer-drivers.md)中所述，根据安装程序 INF 文件提供安装过程。

所有自定义驱动程序代码都必须是可重入的。 用户模式代码应使用 Windows SDK 文档) 中所述 (关键部分对象。 内核模式代码应使用信号量 (参阅 [**EngCreateSemaphore**](/windows/win32/api/winddi/nf-winddi-engcreatesemaphore) 和相关函数) 。

打印机驱动程序和自定义后台处理程序组件必须通过专门为这些驱动程序和后台处理程序组件提供的接口访问注册表，如 WDK 的相应部分所述。

### <a name="installation-considerations"></a>安装注意事项

通常，您只需提供一个 INF 文件，在用户调用 " **添加打印机** 向导" 时，该文件可由 Microsoft 的打印机类安装程序读取。 有时还需要 (共同安装程序或) 安装程序的自定义安装代码。 如果必须创建自定义安装代码，请记住以下事项：

-   用户或安装程序代码必须将终端服务器置于安装模式。  (有关详细信息，请参阅 Microsoft Windows SDK 文档。 ) 

-   不要尝试替换系统文件。 Windows 文件保护禁止系统文件替换。

-   避免需要尽可能多的系统重新启动。 遵循以下指南：
    1.  请勿替换未更改的驱动程序文件。 例如，如果已安装了最新版本，则不应更新多个设备共享的文件。
    2.  如果必须替换文件，安装代码应采取步骤来卸载旧版本，然后加载新版本 (例如，通过停止驱动程序服务、替换文件，然后重新启动服务) 。
    3.  如果要求用户注销，然后重新登录，则最好是需要重新启动系统。

有关共同安装程序和类安装程序的详细信息，请参阅 [编写类安装程序和共同安装程序](../install/writing-class-installers-and-co-installers.md)。

**注意**   编写自定义安装代码之前，请务必阅读 Windows SDK 文档中提供的终端服务编程准则。

 

### <a name="user-interface-considerations"></a>用户界面注意事项

用户运行的自定义安装代码可以显示用户界面。

几乎所有打印机驱动程序代码都在后台处理程序的执行上下文中运行，因此无法显示用户界面。 用户界面只能由打印机接口 Dll 显示，并且只能在以下函数内显示：

-   [**DrvDevicePropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)和 [**DrvDocumentPropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)函数，用于创建属性页。

-   [**DrvPrinterEvent**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)函数，用于接收标识打印机事件的事件代码。 请注意，函数只能显示打印机 \_ 事件 " \_ 添加连接" 和 "打印机事件" " \_ \_ \_ 删除连接" \_ 事件代码的用户界面。

所有其他打印机驱动程序代码都在后台处理程序的上下文中执行。 在此上下文中，允许调用 **MessageBox** 或 **MessageBoxEx** ，但必须设置 MB \_ 服务 \_ 通知。 Windows SDK 文档中介绍了这些函数。

 


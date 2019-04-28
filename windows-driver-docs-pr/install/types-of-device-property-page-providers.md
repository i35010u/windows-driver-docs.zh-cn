---
title: 设备属性页提供程序的类型
description: 设备属性页提供程序的类型
ms.assetid: b467543e-6907-44e5-b407-637cad7f6d78
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ebae27b634f97d95d094f7150283ca86f779b95
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339517"
---
# <a name="types-of-device-property-page-providers"></a>设备属性页提供程序的类型


可以使用以下类型的属性页提供程序来提供自定义设备属性页：

-   **安装程序类和共同安装程序。**

    一个[共同安装程序](writing-a-co-installer.md)通过支持可以提供一个或多个自定义设备属性页[ **DIF_ADDPROPERTYPAGE_ADVANCED** ](https://msdn.microsoft.com/library/windows/hardware/ff543656)设备安装函数 (DIF) 代码。 当安装程序，用于提供属性页句柄**DIF_ADDPROPERTYPAGE_ADVANCED**请求，它设置为属性页对话框过程的地址。

    共同安装程序的 Toaster 示例 Windows Driver Kit (WDK) 中支持这种类型的设备属性页提供程序。 该文件位于*src\\常规\\toaster\\classinstaller* WDK 的子目录。

    有关此类型的提供程序要求的详细信息，请参阅[设备属性页提供程序 （共同安装程序） 的特定要求](specific-requirements-for-device-property-page-providers--class-instal.md)。

    **请注意**  虽然可以编写自定义设备的属性页提供的类安装程序，但它是通常最好提供此功能在共同安装程序，以及其他特定于设备或设备类特定功能。

     

-   **属性页扩展 DLL。**

    提供了一个或多个自定义设备属性页的 DLL 被称为*属性页扩展 DLL*。 这种类型的提供程序通过实现来支持自定义属性页**AddPropSheetPageProc、 ExtensionPropSheetPageProc**，和其他属性表回调函数。 有关这些函数的详细信息，请参阅 Microsoft Windows 软件开发工具包 (SDK) for Windows 7 和.NET Framework 4.0 的文档。

    此类型提供程序的安装通过指定**EnumPropPages32**中的条目*添加注册表部分*的[ **INF AddReg 指令**](inf-addreg-directive.md). 中指定此指令[ **INF *DDInstall*部分**](inf-ddinstall-section.md)。

    AC97 示例音频驱动程序支持此类型的设备属性页提供程序。 该文件位于*src\\音频\\ac97* WDK 的子目录。

    有关此类型的提供程序要求的详细信息，请参阅[设备属性页提供程序 (属性页扩展 Dll) 的特定要求](specific-requirements-for-device-property-page-providers--property-pag.md)。

    **请注意**  除非你[驱动程序包](driver-packages.md)需要类安装程序或辅助安装程序支持自定义设备属性页，通过使用属性页扩展 DLL 效率更高。

     

所有类型的设备属性页提供程序必须都遵循中所述的准则[设备属性页提供程序的常规要求](general-requirements-for-device-property-page-providers.md)。

 

 






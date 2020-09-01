---
title: 设备属性页提供程序的类型
description: 设备属性页提供程序的类型
ms.assetid: b467543e-6907-44e5-b407-637cad7f6d78
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 221449bfbde6c09946b2a3a4343a8b7c1601474c
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097351"
---
# <a name="types-of-device-property-page-providers"></a>设备属性页提供程序的类型


您可以使用以下类型的属性页提供程序来提供自定义设备属性页：

-   **类安装程序和共同安装程序。**

    [共同安装程序](writing-a-co-installer.md)可以通过支持[**DIF_ADDPROPERTYPAGE_ADVANCED**](./dif-addpropertypage-advanced.md)设备安装功能 (DIF) 代码提供一个或多个自定义设备属性页。 当提供属性页的安装程序处理 **DIF_ADDPROPERTYPAGE_ADVANCED** 请求时，它会为属性页设置对话框过程的地址。

    Windows 驱动程序工具包 (WDK) 中 Toaster 示例的一部分的共同安装程序支持这种类型的设备属性页提供程序。 它位于 WDK 的 *src \\ general \\ toaster \\ classinstaller* 子目录中。

    有关此类提供程序的要求的详细信息，请参阅 [设备属性页提供程序的特定要求 (共同安装程序) ](specific-requirements-for-device-property-page-providers--class-instal.md)。

    **注意**   尽管可以编写提供自定义设备属性页的类安装程序，但通常更好的做法是在共同安装程序中提供此功能，以及其他特定于设备或特定于设备的功能。

     

-   **属性页扩展 DLL。**

    提供一个或多个自定义设备属性页的 DLL 称为 *属性页扩展 DLL*。 这种类型的提供程序通过实现 **AddPropSheetPageProc、ExtensionPropSheetPageProc**和其他属性表回调函数支持自定义属性页。 有关这些函数的详细信息，请参阅适用于 Windows 7 的 Microsoft Windows 软件开发工具包 (SDK) 和 .NET Framework 4.0 文档。

    这种类型的提供程序是通过在[**INF AddReg 指令**](inf-addreg-directive.md)的 "*添加注册表" 部分*中指定**EnumPropPages32**项安装的。 此指令在 [**INF *DDInstall* 部分**](inf-ddinstall-section.md)中指定。

    AC97 示例音频驱动程序支持这种类型的设备属性页提供程序。 它位于 WDK 的 *src \\ 音频 \\ ac97* 子目录中。

    有关此类提供程序的要求的详细信息，请参阅 [) 的设备属性页提供程序 (的特定要求 ](specific-requirements-for-device-property-page-providers--property-pag.md)。

    **注意**   除非您的[驱动程序包](driver-packages.md)需要类安装程序或共同安装程序，否则通过使用属性页扩展 DLL，更有效地支持自定义设备属性页。

     

所有类型的设备属性页提供程序必须遵循 [设备属性页提供程序一般要求](general-requirements-for-device-property-page-providers.md)中所述的指导原则。

 


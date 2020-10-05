---
title: 设备属性页概述
description: 设备属性页概述
ms.assetid: b117721a-db32-4144-b0ae-5a0fca40f9db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5214ccf61c5de7c4e3ae836647f8c4f875bcb0a
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733252"
---
# <a name="overview-of-device-property-pages"></a>设备属性页概述


*设备属性页*是允许用户查看和编辑设备属性的窗口。 对于大多数设备，操作系统提供标准的设备属性页，允许用户查看和编辑该设备的一组常用参数。 有关如何为设备显示属性页的详细信息，请参阅 [设备属性页的显示方式](how-device-property-pages-are-displayed.md)。

独立硬件供应商 (Ihv) 通常会提供自定义设备属性页面，使用户能够查看和编辑设备的附加属性和专有属性。 这些属性特定于 IHV 提供的每个设备。 这些属性可能包含用于调制解调器的 CD 驱动器或扬声器音量的默认播放音量。

IHV 使用属性页提供程序创建自定义设备属性页。 属性页提供程序可以是下列项之一：

<a href="" id="class-installers-and-co-installers"></a>**类安装程序和共同安装程序**  
辅助安装程序或类安装程序可以通过支持 DIF_ADDPROPERTYPAGE_ADVANCED 设备安装功能 (DIF) 代码提供一个或多个自定义设备属性页。

<a href="" id="property-page-extension-dll"></a>**属性页扩展 DLL**  
提供一个或多个自定义设备属性页的动态链接库 (DLL) 称为 *属性页扩展 DLL*。 这种类型的提供程序通过实现 **AddPropSheetPageProc**、 **ExtensionPropSheetPageProc**和其他属性表回调函数支持自定义属性页。

有关这些函数的详细信息，请参阅适用于 Windows 7 的 Microsoft Windows 软件开发工具包 (SDK) 和 .NET Framework 4.0。

如果 IHV 的设备或设备类具有用户可以设置的任何单个属性，则 IHV 应在其驱动程序包中提供自定义设备属性页的提供程序。

**注意**   在早于 Windows 2000 的 Windows 版本中，用户在 "控制面板" 中设置了此类信息。 为 Windows 2000 和更高版本的 Windows 编写的驱动程序软件应改为提供属性页。

 

有关属性页提供程序的详细信息，请参阅 [设备属性页提供程序的类型](types-of-device-property-page-providers.md)。

Windows 7 和 .NET Framework 4.0 文档的 Windows SDK 提供了有关属性页和操作这些页的 Microsoft Win32 函数的综合指导。 有关属性页和属性表的详细信息，请参阅适用于 Windows 7 的 Windows SDK 中的 [属性表](/windows/win32/controls/property-sheet-reference) 和 .NET Framework 4.0 文档。

 


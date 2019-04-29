---
title: 设备属性页概述
description: 设备属性页概述
ms.assetid: b117721a-db32-4144-b0ae-5a0fca40f9db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec451c9885886f57c61489a7727a1f093daf8d53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369449"
---
# <a name="overview-of-device-property-pages"></a>设备属性页概述


一个*设备属性页*是一个窗口，允许用户查看和编辑设备属性。 适用于大多数设备操作系统提供标准版设备允许用户查看和编辑一组通用的参数为该设备的属性页。 有关设备的属性页的显示方式的详细信息，请参阅[如何设备属性页会显示](how-device-property-pages-are-displayed.md)。

独立硬件供应商 (Ihv) 通常提供允许用户查看和编辑其他和专有的设备的属性的自定义设备属性页。 这些属性是特定于 IHV 提供每个设备。 这些属性可能包含默认播放的 CD 驱动器卷或调制解调器的扬声器音量。

IHV 通过属性页提供程序来创建自定义设备属性页。 属性页提供程序可以是以下值之一：

<a href="" id="class-installers-and-co-installers"></a>**安装程序类和共同安装程序**  
辅助安装程序或类的安装程序可以通过支持 DIF_ADDPROPERTYPAGE_ADVANCED 设备安装函数 (DIF) 代码提供一个或多个自定义设备属性页。

<a href="" id="property-page-extension-dll"></a>**属性页扩展 DLL**  
提供了一个或多个自定义设备属性页的动态链接库 (DLL) 被称为*属性页扩展 DLL*。 这种类型的提供程序通过实现来支持自定义属性页**AddPropSheetPageProc**， **ExtensionPropSheetPageProc**，和其他属性表回调函数。

有关这些函数的详细信息，请参阅适用于 Windows 7 和.NET Framework 4.0 的 Microsoft Windows 软件开发工具包 (SDK)。

IHV 应提供其驱动程序包中的自定义设备属性页的提供程序，如果其设备或设备类具有任何用户可以设置的单个属性。

**请注意**  在版本的 Windows 早于 Windows 2000，用户所设置的控制面板中的此类信息。 为 Windows 2000 和更高版本的 Windows 编写的驱动程序软件应改为提供属性页。

 

有关属性页提供程序的详细信息，请参阅[类型的设备属性页提供程序](types-of-device-property-page-providers.md)。

Windows SDK 适用于 Windows 7 和.NET Framework 4.0 文档提供了有关属性页和对其进行处理的 Microsoft Win32 函数的全面指导。 有关属性页和属性表的详细信息，请参阅[属性表](https://go.microsoft.com/fwlink/p/?linkid=180781)Windows SDK 适用于 Windows 7 和.NET Framework 4.0 文档中。

 

 






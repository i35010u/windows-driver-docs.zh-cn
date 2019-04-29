---
title: 添加新的属性表页
description: 添加新的属性表页
ms.assetid: ec4303e9-889c-41ee-8872-ddefdc906eb2
keywords:
- 用户界面插件 WDK 打印，属性表页
- UI 插件 WDK 打印，属性表页
- 属性表页 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 884ec86b72b32f10aa8d0262614eb09b862523dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354095"
---
# <a name="adding-new-property-sheet-pages"></a>添加新的属性表页





如果你想要将新页面添加到 Unidrv 或 Pscript5、 UI 插件提供的打印机接口的属性表必须实现以下 IPrintOemUI 方法：

-   [**IPrintOemUI::DevicePropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff554165)

    用于将添加到打印机属性页中，当用户选择显示**属性**菜单项从打印机文件夹或打印机窗口中，或当应用程序调用 PrinterProperties 函数 (中所述Windows SDK 文档）。

-   [**IPrintOemUI::DocumentPropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff554173)

    用于将页面添加到文档属性页中，当用户选择显示**打印机首选项**菜单项从打印机文件夹或打印机窗口中，或当应用程序调用 DocumentProperties 或AdvancedDocumentProperties 函数 （Windows SDK 文档中所述）。

如果你实现以下方法之一，则将通常还提供[  **\_CPSUICALLBACK**](https://msdn.microsoft.com/library/windows/hardware/ff564313)-类型化回调函数来处理用户做出的修改。 必须调用此回调函数[ **IPrintOemDriverUI::DrvUpdateUISetting** ](https://msdn.microsoft.com/library/windows/hardware/ff553115)通知驱动程序时已修改与用户界面设置关联的值，如果设置的值是存储在驱动程序的[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构或注册表项。

 

 





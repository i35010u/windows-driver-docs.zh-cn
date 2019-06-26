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
ms.openlocfilehash: c1e0fd82cc541294ed69ea723c280fee1ceb34ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370502"
---
# <a name="adding-new-property-sheet-pages"></a>添加新的属性表页





如果你想要将新页面添加到 Unidrv 或 Pscript5、 UI 插件提供的打印机接口的属性表必须实现以下 IPrintOemUI 方法：

-   [**IPrintOemUI::DevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)

    用于将添加到打印机属性页中，当用户选择显示**属性**菜单项从打印机文件夹或打印机窗口中，或当应用程序调用 PrinterProperties 函数 (中所述Windows SDK 文档）。

-   [**IPrintOemUI::DocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)

    用于将页面添加到文档属性页中，当用户选择显示**打印机首选项**菜单项从打印机文件夹或打印机窗口中，或当应用程序调用 DocumentProperties 或AdvancedDocumentProperties 函数 （Windows SDK 文档中所述）。

如果你实现以下方法之一，则将通常还提供[  **\_CPSUICALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-_cpsuicallback)-类型化回调函数来处理用户做出的修改。 必须调用此回调函数[ **IPrintOemDriverUI::DrvUpdateUISetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting)通知驱动程序时已修改与用户界面设置关联的值，如果设置的值是存储在驱动程序的[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构或注册表项。

 

 





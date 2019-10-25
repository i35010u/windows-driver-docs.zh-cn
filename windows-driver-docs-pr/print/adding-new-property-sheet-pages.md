---
title: 添加新的属性表页
description: 添加新的属性表页
ms.assetid: ec4303e9-889c-41ee-8872-ddefdc906eb2
keywords:
- 用户界面插件 WDK 打印，属性表页面
- UI 插件 WDK 打印，属性表单页面
- 属性表页 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e14ef057b94ec7d0ffdb43064c635b40f60a805
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843263"
---
# <a name="adding-new-property-sheet-pages"></a>添加新的属性表页





如果要向 Unidrv 或 Pscript5 的打印机接口提供的属性表添加新页面，UI 插件必须实现以下 IPrintOemUI 方法：

-   [**IPrintOemUI：:D evicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)

    用于添加到打印机属性表，当用户从打印机文件夹或打印机窗口中选择 "**属性**" 菜单项时，或者当应用程序调用 PrinterProperties 函数时（在 Windows SDK 文档中介绍），将显示该属性表.

-   [**IPrintOemUI：:D ocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)

    用于将页面添加到文档属性表，当用户从打印机文件夹或打印机窗口中选择**打印机首选项**菜单项时，或者当应用程序调用 DocumentProperties 或 AdvancedDocumentProperties 时，将显示此页。函数（如 Windows SDK 文档中所述）。

如果实现其中一种方法，通常还会提供[ **\_CPSUICALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)类型的回调函数来处理用户修改。 如果与用户界面设置关联的值已修改（如果设置的值存储在驱动程序的[**DEVMODEW**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构中），则此回调函数必须调用[**IPrintOemDriverUI：:D rvupdateuisetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting)以通知驱动程序注册表项。

 

 





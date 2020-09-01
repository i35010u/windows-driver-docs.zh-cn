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
ms.openlocfilehash: 8cddac41a727be322bb7fc281e728436949c32bc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218276"
---
# <a name="adding-new-property-sheet-pages"></a>添加新的属性表页





如果要向 Unidrv 或 Pscript5 的打印机接口提供的属性表添加新页面，UI 插件必须实现以下 IPrintOemUI 方法：

-   [**IPrintOemUI：:D evicePropertySheets**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)

    用于添加到打印机属性表，当用户从打印机文件夹或打印机窗口中选择 " **属性** " 菜单项时，或者当应用程序调用 PrinterProperties 函数时，它将在 Windows SDK 文档) 中 (说明的情况下显示。

-   [**IPrintOemUI：:D ocumentPropertySheets**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)

    用于将页面添加到文档属性表中，当用户从打印机文件夹或打印机窗口中选择 **打印机首选项** 菜单项时，或者当应用程序调用 DocumentProperties 或 AdvancedDocumentProperties 函数时，这些页面将在 Windows SDK 文档) 中 (所述。

如果实现其中一种方法，通常还会提供[** \_ CPSUICALLBACK**](/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)类型的回调函数来处理用户修改。 如果与用户界面设置关联的值已修改（如果设置的值存储在驱动程序的[**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew)结构或注册表项中），则此回调函数必须调用[**IPrintOemDriverUI：:D rvupdateuisetting**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting)以通知驱动程序。

 


---
title: 为打印机创建属性表页
description: 为打印机创建属性表页
keywords:
- 打印机接口 DLL WDK，属性表页
- 属性表页 WDK 打印，创建
- 属性表页 WDK 打印，打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9da3fa9a1f956382b0658dd9f9ceab578940aec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797453"
---
# <a name="creating-property-sheet-pages-for-printers"></a>为打印机创建属性表页





与 [CPSUI](common-property-sheet-user-interface.md)一起使用的打印机接口 dll 负责创建 Windows 2000 和更高版本的用户用于查看和修改与打印机和打印文档关联的配置参数的属性表页。 每个打印机接口 DLL 都必须提供 [**DrvDevicePropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets) 函数来创建打印机特定的页面，并提供 [**DrvDocumentPropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets) 函数来创建特定于文档的页面。

若要了解如何设计这些函数，请务必阅读描述 [CPSUI](common-property-sheet-user-interface.md)的部分。 显示属性表页面涉及应用程序、打印后台处理程序、打印机接口 DLL 和 CPSUI 之间的交互。 [使用 CPSUI 和打印机驱动程序](using-cpsui-with-printer-drivers.md)中介绍了执行流。

 


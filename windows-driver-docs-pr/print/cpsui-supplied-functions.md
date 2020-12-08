---
title: CPSUI 提供的函数
description: CPSUI 提供的函数
keywords:
- 公共属性表用户界面 WDK 打印，功能
- CPSUI WDK 打印，函数
- 属性表页 WDK 打印，函数
- 函数 WDK CPSUI
- CommonPropertySheetUI
- ComPropSheet
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6585e287135660468b0931f4013e572e22443fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797481"
---
# <a name="cpsui-supplied-functions"></a>CPSUI 提供的函数





CPSUI 为应用程序提供了以下两个重要功能：

-   [**CommonPropertySheetUI**](/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)

    [**CommonPropertySheetUI**](/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)函数是 CPSUI 的入口点。 函数会导致创建并显示属性页页面，然后允许用户查看和修改它们。

    当应用程序调用 [**CommonPropertySheetUI**](/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)时，它将提供 [页面创建回调](page-creation-callbacks.md) 的地址，用于描述要创建的页面。 CPSUI 调用此回调以获取页面说明。 然后，它会显示页面，使应用程序用户可以修改该页中包含的值，并使用 [页面事件回调](page-event-callbacks.md)将修改后的值传递到应用程序。 在用户通过单击 **"确定" 或 "** 取消" 来 **取消** 属性表之前， **CommonPropertySheetUI** 函数不会返回。

    请注意，打印机接口 Dll 不调用此函数;它由打印后台处理程序调用。

-   [**ComPropSheet**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)

    [**ComPropSheet**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)函数指的是应用程序将属性表页描述为 CPSUI 的方法，以便 CPSUI 可以创建并显示它们。 CPSUI 应用程序从 [页创建回调](page-creation-callbacks.md)中调用此函数。 通常，页面说明包含指向 [页面事件回调](page-event-callbacks.md)的指针，当应用程序用户修改页面值时，CPSUI 将调用该指针。

有关这些函数的调用时间的详细说明，请参阅将 [CPSUI 与打印机驱动程序配合使用](using-cpsui-with-printer-drivers.md)。

应用程序提供的对话框过程可以使用另外两个 CPSUI 提供的函数（ [**SetCPSUIUserData**](/windows-hardware/drivers/ddi/compstui/nf-compstui-setcpsuiuserdata) 和 [**GetCPSUIUserData**](/windows-hardware/drivers/ddi/compstui/nf-compstui-getcpsuiuserdata)）来存储和检索应用程序提供的值。

 


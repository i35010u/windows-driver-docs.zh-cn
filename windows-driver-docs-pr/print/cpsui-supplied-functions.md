---
title: CPSUI 提供的函数
description: CPSUI 提供的函数
ms.assetid: 49da252a-fb51-43f3-b2e8-27253470b4b5
keywords:
- 常用属性页用户界面 WDK 打印，函数
- CPSUI WDK 打印，函数
- 属性表页 WDK 打印函数
- WDK CPSUI 函数
- CommonPropertySheetUI
- ComPropSheet
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a322d252fd40d8b85afff9c9f644355fbc2f6b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372443"
---
# <a name="cpsui-supplied-functions"></a>CPSUI 提供的函数





CPSUI 为应用程序提供以下两个重要函数：

-   [**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia)

    [ **CommonPropertySheetUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia)函数是 CPSUI 的入口点。 该函数将导致属性表页创建和显示，然后使他们可以查看和修改的用户。

    当应用程序调用[ **CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia)，它提供的地址[页创建回调](page-creation-callbacks.md)，它描述要创建的页面。 CPSUI 调用此回调以获取页说明。 然后，它显示页面，应用程序用户可以修改包含在页中，值并将修改应用程序使用的值[页上的事件的回调](page-event-callbacks.md)。 **CommonPropertySheetUI**函数不会返回直到用户已单击关闭属性表**确定**或**取消**。

    请注意该打印机接口 Dll 不调用此函数;它是由打印后台处理程序调用。

-   [**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)

    [ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)函数是依据应用程序描述 CPSUI，到属性表页，以便 CPSUI 可以创建并显示它们的方式。 CPSUI 应用程序中调用此函数[页上创建回叫](page-creation-callbacks.md)。 通常情况下，页说明内容包括一个指向[页面事件回调](page-event-callbacks.md)，后者 CPSUI 会调用时，应用程序用户修改页的值。

当调用这些函数的详细说明，请参阅[与打印机驱动程序使用 CPSUI](using-cpsui-with-printer-drivers.md)。

两个其他 CPSUI 提供函数， [ **SetCPSUIUserData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-setcpsuiuserdata)并[ **GetCPSUIUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-getcpsuiuserdata)，可以由应用程序提供对话框框过程来存储和检索应用程序提供的值。

 

 





---
title: 对话框过程和 CPSUI
description: 对话框过程和 CPSUI
ms.assetid: fad65a34-9580-41a5-ad58-91ea7ffcd3d5
keywords:
- 页面事件回调 WDK CPSUI
- 事件的回调 WDK CPSUI
- 消息处理程序 WDK CPSUI
- CPSUI WDK 打印，消息处理程序
- 对话框框过程 WDK CPSUI
- 窗口消息 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b50d323ebdec809f5e033437634561f8514dc2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360209"
---
# <a name="dialog-box-procedures-and-cpsui"></a>对话框过程和 CPSUI





对话框过程是用于处理窗口消息系统发送的回调函数。 这种类型的[页上的事件回调](page-event-callbacks.md)是必需的如果要创建未提供的 CPSUI 的自定义的属性表页。 (还可以使用对话框框中使用的过程[CPSUI 提供页和模板](cpsui-supplied-pages-and-templates.md)，但使用的[CPSUI 消息处理程序](cpsui-message-handler.md)建议。)有关对话框框中过程的详细信息，请参阅 Microsoft Windows SDK 文档中的 DialogProc。 使用 DLGPROC 指针类型，还介绍了 Windows SDK 文档中声明指向对话框框中的过程。

有关使用 CPSUI 创建的所有属性表页，窗口消息是第一次被截获 CPSUI 传递到应用程序提供的对话框过程之前。 如果使用 CPSUI 提供模板定义页面，应用程序提供的对话框过程可以提供一个返回值，该值 CPSUI 应处理该消息。

可以使用对话框过程[ **SetCPSUIUserData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-setcpsuiuserdata)并[ **GetCPSUIUserData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-getcpsuiuserdata)函数来存储和检索应用程序提供的值。

有关使用随 CPSUI 对话框框中过程的详细信息，请参阅备注部分[ **DLGPAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_dlgpage)。

 

 





---
title: 对话框过程和 CPSUI
description: 对话框过程和 CPSUI
ms.assetid: fad65a34-9580-41a5-ad58-91ea7ffcd3d5
keywords:
- 页面事件回调 WDK CPSUI
- 事件回调 WDK CPSUI
- 消息处理程序 WDK CPSUI
- CPSUI WDK 打印，消息处理程序
- 对话框过程 WDK CPSUI
- 窗口消息 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c22be1b6faa75d85dd287e61bd3e9791578c6d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828919"
---
# <a name="dialog-box-procedures-and-cpsui"></a>对话框过程和 CPSUI





对话框过程是处理系统发送的窗口消息的回调函数。 如果创建的自定义属性表页不是由 CPSUI 提供的，则需要此类型的[页事件回调](page-event-callbacks.md)。 （还可以将对话框过程用于[CPSUI 提供的页面和模板](cpsui-supplied-pages-and-templates.md)，但建议使用[CPSUI 消息处理程序](cpsui-message-handler.md)。）有关对话框过程的详细信息，请参阅 Microsoft Windows SDK 文档中的 DialogProc。 指向对话框过程的指针使用 DLGPROC 指针类型进行声明，也在 Windows SDK 文档中进行了介绍。

对于使用 CPSUI 创建的所有属性表页，先通过 CPSUI 截获窗口消息，然后再将其传递到应用程序提供的对话框过程。 如果该页是使用 CPSUI 提供的模板定义的，则应用程序提供的对话框过程可以提供一个返回值，指示 CPSUI 应处理该消息。

对话框过程可以使用[**SetCPSUIUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-setcpsuiuserdata)和[**GetCPSUIUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-getcpsuiuserdata)函数来存储和检索应用程序提供的值。

有关将对话框过程用于 CPSUI 的详细信息，请参阅[**DLGPAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)的 "备注" 部分。

 

 





---
title: 页面事件回调
description: 页面事件回调
keywords:
- 回调函数 WDK CPSUI
- 公共属性表用户界面 WDK 打印，回调
- CPSUI WDK 打印，回调
- 属性表页 WDK 打印，回调
- 页面事件回调 WDK CPSUI
- 事件回调 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 515b5f2954e381d29820b1972a91595b4d89ac46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807657"
---
# <a name="page-event-callbacks"></a>页面事件回调





当用户与属性表页面交互时，操作系统会将此类窗口事件的通知发送为已更改的焦点或修改后的值。 CPSUI 应用程序如何接收页面的窗口事件的通知取决于应用程序如何定义该页：

-   如果已使用 [CPSUI 提供的页面和模板](cpsui-supplied-pages-and-templates.md)定义了页面，则可以提供 [CPSUI 消息处理程序](cpsui-message-handler.md)。

-   如果应用程序创建了 CPSUI 未提供的自定义页，则它必须提供对话框过程。 有关详细信息，请参阅 [对话框过程和 CPSUI](dialog-box-procedures-and-cpsui.md)。

当 CPSUI 应用程序调用 [**ComPropSheet**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet) 函数时，它会向 CPSUI 提供页面事件回调的地址。

 


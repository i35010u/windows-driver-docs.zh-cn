---
title: 页面事件回调
description: 页面事件回调
ms.assetid: 891f62ec-d009-42c8-8143-73bfe737a946
keywords:
- 回调函数 WDK CPSUI
- 公共属性表用户界面 WDK 打印，回调
- CPSUI WDK 打印，回调
- 属性表页 WDK 打印，回调
- 页面事件回调 WDK CPSUI
- 事件回调 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a440a4f5ee9910ae982304c6739447fffcf4f4c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845047"
---
# <a name="page-event-callbacks"></a>页面事件回调





当用户与属性表页面交互时，操作系统会将此类窗口事件的通知发送为已更改的焦点或修改后的值。 CPSUI 应用程序如何接收页面的窗口事件的通知取决于应用程序如何定义该页：

-   如果已使用[CPSUI 提供的页面和模板](cpsui-supplied-pages-and-templates.md)定义了页面，则可以提供[CPSUI 消息处理程序](cpsui-message-handler.md)。

-   如果应用程序创建了 CPSUI 未提供的自定义页，则它必须提供对话框过程。 有关详细信息，请参阅[对话框过程和 CPSUI](dialog-box-procedures-and-cpsui.md)。

当 CPSUI 应用程序调用[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)函数时，它会向 CPSUI 提供页面事件回调的地址。

 

 





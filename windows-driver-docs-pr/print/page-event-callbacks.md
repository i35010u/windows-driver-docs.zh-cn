---
title: 页面事件回调
description: 页面事件回调
ms.assetid: 891f62ec-d009-42c8-8143-73bfe737a946
keywords:
- 回调函数 WDK CPSUI
- 常用属性页用户界面 WDK 打印，回调
- CPSUI WDK 打印，回调
- 属性表页 WDK 打印回调
- 页面事件回调 WDK CPSUI
- 事件的回调 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c262a174865348acecc70f36c614c065aa2731bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566195"
---
# <a name="page-event-callbacks"></a>页面事件回调





当用户与属性表页交互时，操作系统发送此类窗口事件的通知为已更改的焦点或修改后的值。 CPSUI 应用程序接收通知的页面的窗口事件的方式取决于应用程序具有定义页的方式：

-   如果使用定义页，则[CPSUI 提供页和模板](cpsui-supplied-pages-and-templates.md)，它可以提供[CPSUI 消息处理程序](cpsui-message-handler.md)。

-   如果应用程序创建自定义的页面 CPSUI 不提供，它必须提供对话框过程。 有关详细信息，请参阅[对话框框过程和 CPSUI](dialog-box-procedures-and-cpsui.md)。

CPSUI 应用程序的页面事件回调的地址在它调用时都提供 CPSUI [ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)函数。

 

 





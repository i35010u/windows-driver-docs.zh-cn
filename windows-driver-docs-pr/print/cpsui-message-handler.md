---
title: CPSUI 消息处理程序
description: CPSUI 消息处理程序
ms.assetid: 4a6434e9-d65e-4ddd-836e-d6101532bbb8
keywords:
- 页面事件回调 WDK CPSUI
- 事件的回调 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82338185b587b89432686b1f3c0bd28891f2055e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372455"
---
# <a name="cpsui-message-handler"></a>CPSUI 消息处理程序





CPSUI 消息处理程序是使用定义的回调函数[  **\_CPSUICALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-_cpsuicallback)函数类型。 这种类型的[页上的事件回调](page-event-callbacks.md)如果你使用建议[CPSUI 提供页和模板](cpsui-supplied-pages-and-templates.md)。

当用户与属性表页进行交互，并会导致要发生的事件时，CPSUI 截获事件并调用\_CPSUICALLBACK 类型化函数，提供[ **CPSUICBPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_cpsuicbparam)调用的结构，它介绍了回调函数的原因。

回调函数必须处理的事件，并将 status 值再回到 CPSUI，该值指示页需要以重新显示或重新初始化。

 

 





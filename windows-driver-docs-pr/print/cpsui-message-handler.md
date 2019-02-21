---
title: CPSUI 消息处理程序
description: CPSUI 消息处理程序
ms.assetid: 4a6434e9-d65e-4ddd-836e-d6101532bbb8
keywords:
- 页面事件回调 WDK CPSUI
- 事件的回调 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7412023503beac133b921d08a502cf8934ae2ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526786"
---
# <a name="cpsui-message-handler"></a>CPSUI 消息处理程序





CPSUI 消息处理程序是使用定义的回调函数[  **\_CPSUICALLBACK** ](https://msdn.microsoft.com/library/windows/hardware/ff564313)函数类型。 这种类型的[页上的事件回调](page-event-callbacks.md)如果你使用建议[CPSUI 提供页和模板](cpsui-supplied-pages-and-templates.md)。

当用户与属性表页进行交互，并会导致要发生的事件时，CPSUI 截获事件并调用\_CPSUICALLBACK 类型化函数，提供[ **CPSUICBPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff547088)调用的结构，它介绍了回调函数的原因。

回调函数必须处理的事件，并将 status 值再回到 CPSUI，该值指示页需要以重新显示或重新初始化。

 

 





---
title: CPSUI 消息处理程序
description: CPSUI 消息处理程序
ms.assetid: 4a6434e9-d65e-4ddd-836e-d6101532bbb8
keywords:
- 页面事件回调 WDK CPSUI
- 事件回调 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e93e0646df59c2060c30302c46efbfb4ccf5acc4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217791"
---
# <a name="cpsui-message-handler"></a>CPSUI 消息处理程序





CPSUI 消息处理程序是使用[** \_ CPSUICALLBACK**](/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)函数类型定义的回调函数。 如果使用[CPSUI 提供的页面和模板](cpsui-supplied-pages-and-templates.md)，则建议使用这种类型的[页事件回调](page-event-callbacks.md)。

当用户与属性表页交互并导致事件发生时，CPSUI 会截获事件并调用 \_ CPSUICALLBACK 函数，同时提供一个描述调用回调函数原因的 [**CPSUICBPARAM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam) 结构。

回调函数必须处理该事件，然后将状态值返回到 CPSUI，用于指示是否需要重新显示或重新初始化该页。

 


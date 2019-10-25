---
title: CPSUI 消息处理程序
description: CPSUI 消息处理程序
ms.assetid: 4a6434e9-d65e-4ddd-836e-d6101532bbb8
keywords:
- 页面事件回调 WDK CPSUI
- 事件回调 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb7a806527b3e689a47d8c0b4b3828b316a63d50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831810"
---
# <a name="cpsui-message-handler"></a>CPSUI 消息处理程序





CPSUI 消息处理程序是使用[ **\_CPSUICALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)函数类型定义的回调函数。 如果使用[CPSUI 提供的页面和模板](cpsui-supplied-pages-and-templates.md)，则建议使用这种类型的[页事件回调](page-event-callbacks.md)。

当用户与属性表页交互并导致事件发生时，CPSUI 会截获事件并调用 \_CPSUICALLBACK 类型的函数，并提供一个说明回调函数的原因的[**CPSUICBPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam)结构。名.

回调函数必须处理该事件，然后将状态值返回到 CPSUI，用于指示是否需要重新显示或重新初始化该页。

 

 





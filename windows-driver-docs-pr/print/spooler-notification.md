---
title: 后台处理程序通知
description: 后台处理程序通知
ms.assetid: b5d9b909-f2e4-4773-903e-1dd73b0ca567
keywords:
- 后台处理程序通知 WDK 打印
- 打印后台处理程序通知 WDK
- 通知 WDK 打印后台处理程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dff2ef727fc72e50abc1cb76d0b9d08e29b13457
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213635"
---
# <a name="spooler-notification"></a>后台处理程序通知





此功能在 Windows Vista 和更高版本中可用。

后台处理程序通知机制在后台处理程序承载的组件之间提供双向通信路径 (例如打印机驱动程序、打印处理器和端口监视器) 和应用程序。 涉及的应用程序可以在不同的会话和安全上下文中运行。

当打印后台处理程序进程中运行的组件需要在启动打印作业的会话中显示用户界面元素时，后台处理程序通知机制解决了所发生的问题。 在 Windows 2000 及更早版本中，这些打印组件显示的任何 UI 始终显示在会话0中，后台处理程序服务运行的会话。 为帮助解决此问题，为 Windows XP、 [**SplPromptUIInUsersSession**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-splpromptuiinuserssession) 和 [**SplIsSessionZero**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-splissessionzero)添加了两个后台处理程序函数。 后台处理程序通知机制提供了比这些功能更多的功能，这些功能仅限于在对话框中显示消息。

[后台处理程序通知概述](overview-of-spooler-notification.md)

[后台处理程序通知的术语](spooler-notification-terminology.md)

[公共接口](public-interfaces.md)

 


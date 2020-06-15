---
title: 后台处理程序通知的术语
description: 后台处理程序通知的术语
ms.assetid: 7d4888b1-cb5f-4095-9e1b-c330c04e4971
keywords:
- 后台处理程序通知 WDK 打印，术语
- 打印后台处理程序通知 WDK，术语
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 043f619262c8fa2aff9cf2b0caea5562ecd2eb07
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756163"
---
# <a name="spooler-notification-terminology"></a>后台处理程序通知术语

以下术语用于讨论异步后台处理程序通知：

| 术语 | 说明 |
|--|--|
| **回调接口** | 当侦听客户端注册通知时，它必须提供指向[IPrintAsyncNotifyCallback](https://docs.microsoft.com/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifycallback)接口的指针。 通知到达或通道关闭时，将回调此接口的方法。 |
| **侦听客户端** | 已注册用于接收打印通知的应用程序或后台处理程序内部组件。 这不同于之前称为后台处理程序通知管道的客户端。 后台处理程序通知管道的客户端是定义通知类型和架构的任何组件。 |
| **提醒** | 在打印组件和侦听客户端之间通过通知通道发送的数据。 |
| **通知通道** | 逻辑组件。 它由**IPrintAsyncNotifyCallback**接口指针表示。 打印组件在需要发出通知时创建通知通道。 当侦听客户端将数据发送回打印组件时，它将使用通知通道。 |
| **通知注册句柄** | 侦听客户端注册接收通知时由服务创建的句柄。 侦听客户端可以使用此句柄来注销通知。 |
| **打印组件** | 由 Spoolsv.exe 加载的组件，如打印处理器、驱动程序和监视器。 |
| **服务** | 由后台处理程序实现的功能，既可以作为服务本身的一部分（Spoolsv.exe），也可以作为客户端（Winspool.drv. winspool.drv）的一部分。 |

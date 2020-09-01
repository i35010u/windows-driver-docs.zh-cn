---
title: 注册以接收通知
description: 注册以接收通知
ms.assetid: 2442c204-c9d8-49fa-93ae-02623d08119c
keywords:
- 后台处理程序通知 WDK 打印，注册接收
- 打印后台处理程序通知 WDK，注册以接收
- 接收后台处理程序通知
- 注册后台处理程序通知
- RegisterForPrintAsyncNotifications
- UnRegisterForPrintAsyncNotifications
- 取消注册后台处理程序通知
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: db76a13cc12baaa44e392cf481c6c3a6fb9d50a1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216344"
---
# <a name="registering-to-receive-notifications"></a>注册以接收通知

侦听客户端调用 [RegisterForPrintAsyncNotifications](/windows/win32/api/prnasnot/nf-prnasnot-registerforprintasyncnotifications) 方法来注册接收通知。 侦听客户端可以是应用程序，也可以在后台处理程序中运行。 Winspool.drv winspool.drv 公开此功能，而不考虑它的加载位置。

Spoolss 将公开此功能，以便端口监视器可以注册通知。 在后台处理程序中运行并且链接到 Spoolss 的组件可以调用 **RegisterForPrintAsyncNotifications**。 下面的过程详细说明必须在调用此函数时传递的信息。 该过程的第一步适用于第一个参数，第二个步骤适用于第二个参数，依此类推。

```cpp
HRESULT
 RegisterForPrintAsyncNotifications(
    IN LPCWSTR,
    IN PrintAsyncNotificationType*,
    IN PrintAsyncNotifyUserFilter,
    IN PrintAsyncNotifyConversationStyle,
    IN IPrintAsyncNotifyCallback*,
    OUT HANDLE*
    );
```

若要注册通知，请指定以下各项：

1. 本地/远程打印机或服务器名称。

1. 侦听器感兴趣的通知类型。

1. 用户筛选器，指示客户端要接收通知的用户，该用户是通知发件人的用户，也可能是所有用户。

1. 会话样式筛选器。 客户端可以指定单向或双向通信。

1. 当通知从通道的另一端返回时要调用的 [IPrintAsyncNotifyCallback](/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifycallback) 接口。 此参数不能为 **NULL**。

此函数返回时，类型 HANDLE (的第六个参数 \*) 指向注册句柄。 注册句柄是客户端接收的不透明结构。 注册与发出注册调用的线程的用户标识相关联。 后台处理程序根据通道的会话筛选器和客户端的注册会话来筛选侦听客户端，以及客户端会话的筛选器。

若要通知后台处理程序，侦听客户端不应再收到通知，则客户端在调用 [UnRegisterForPrintAsyncNotifications](/windows/win32/api/prnasnot/nf-prnasnot-unregisterforprintasyncnotifications)时必须使用此句柄。 对于单向通信，会消除服务器端上的任何挂起的通知。 对于双向通信，如果有开放式双向通道，通信将继续，直到它们关闭。

```cpp
HRESULT
 UnRegisterForPrintAsyncNotifications(
    IN HANDLE
    );
```
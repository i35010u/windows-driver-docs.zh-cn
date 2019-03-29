---
title: 注册以接收通知
description: 注册以接收通知
ms.assetid: 2442c204-c9d8-49fa-93ae-02623d08119c
keywords:
- 后台处理程序 WDK 打印，注册以接收通知
- 打印后台处理程序 WDK，注册以接收通知
- 后台处理程序通知的接收
- 注册的后台处理程序通知
- RegisterForPrintAsyncNotifications
- UnRegisterForPrintAsyncNotifications
- 取消注册的后台处理程序通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98b168fd0117921d70f043e25039663628f4d3da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569134"
---
# <a name="registering-to-receive-notifications"></a>注册以接收通知





侦听客户端调用[RegisterForPrintAsyncNotifications](https://go.microsoft.com/fwlink/p/?linkid=124752)方法来注册接收通知。 侦听客户端可以是应用程序，也可以在后台处理程序内运行。 Winspool.drv 公开此功能而不考虑其中是加载。

Spoolss.lib 公开此功能，以便可以注册通知的端口监视器。 在后台处理程序内的运行组件和可以调用该链接到 Spoolss.lib **RegisterForPrintAsyncNotifications**。 以下过程详细说明了必须对此函数的调用中传递的信息。 该过程的第一步应用于第一个参数，第二个步骤适用于第二个参数，依此类推。

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

**若要注册通知，请指定**

1.  本地/远程打印机或服务器名称。

2.  侦听器处于感兴趣的通知的类型。

3.  用户筛选器，指示的用户从其客户端是希望接收通知，或者作为通知发送相同的用户或所有用户。

4.  会话样式筛选器。 客户端可以指定单向或双向通信。

5.  [IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)接口从通道另一端返回一条通知时调用。 此参数不能**NULL**。

当此函数返回时，第六个参数 (类型句柄的\*) 指向的注册句柄。 注册句柄是客户端收到的不透明结构。 注册是线程的与进行注册调用的用户标识相关联。 后台处理程序筛选侦听客户端根据频道的会话筛选器和客户端的注册会话中，除了该客户端会话的筛选器。

通知后台处理程序，侦听客户端应不会再收到通知，调用时，客户端必须使用此句柄[UnRegisterForPrintAsyncNotifications](https://go.microsoft.com/fwlink/p/?linkid=124754)。 对于单向通信，解除服务器端上任何挂起的通知。 对于双向通信，如果有打开的双向通道，通信将持续至在关闭为止。

```cpp
HRESULT
 UnRegisterForPrintAsyncNotifications(
    IN HANDLE
    );
```









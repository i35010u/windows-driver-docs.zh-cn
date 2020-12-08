---
title: 通知筛选和通信样式
description: 通知筛选和通信样式
keywords:
- 后台处理程序通知 WDK 打印，筛选
- 打印后台处理程序通知 WDK，筛选
- 通知筛选 WDK 打印后台处理程序
- 筛选 WDK 后台处理程序通知
- CreatePrintAsyncNotifyChannel
- RegisterForPrintAsyncNotifications
- 通知数据类型 WDK 打印后台处理程序
- 数据类型 WDK 后台处理程序通知
- 通信 WDK 后台处理程序通知
- 所有侦听器通知 WDK 打印后台处理程序
- 每用户侦听器筛选 WDK 后台处理程序通知
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: ae16a1659c736c9a5bb5ce7dc558fc481aabdaa1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807773"
---
# <a name="notification-filtering-and-communication-styles"></a>通知筛选和通信样式

本部分介绍了后台处理程序进程和打印组件（如打印处理器、驱动程序和监视器）之间的接口。

## <a name="notification-filtering"></a>通知筛选

PrintAsyncNotifyUserFilter 枚举类型用于两种情况。 在其中的第一个中，后台处理程序中运行的打印组件会调用 [CreatePrintAsyncNotifyChannel](/windows/win32/api/prnasnot/nf-prnasnot-createprintasyncnotifychannel) 函数来创建通知通道。 调用方传递一个 PrintAsyncNotifyUserFilter 枚举类型的枚举器，以指定允许哪些侦听客户端接收通知。 在第二种情况下，侦听客户端将调用 [RegisterForPrintAsyncNotifications](/windows/win32/api/prnasnot/nf-prnasnot-registerforprintasyncnotifications) 函数以注册通知。 调用方传递一个 PrintAsyncNotifyUserFilter 枚举器来指示它应接收的通知。

```cpp
typedef enum
{
  kPerUser,
  kAllUsers
} PrintAsyncNotifyUserFilter;
```

在下图中， **kPerUser** 枚举器用于调用 **CreatePrintAsyncNotifyChannel** 函数。 因此，只允许与进行注册的用户在同一用户帐户中运行的那些侦听器接收通知。

![说明每用户侦听器筛选的关系图](images/notifyfilt1.gif)

在下图中，在对 **CreatePrintAsyncNotifyChannel** 函数的调用中使用 **kAllUsers** 枚举器。 因此，对打印机或服务器感兴趣的所有侦听器都可以接收通知。 请注意，只有管理员才允许在对此函数的调用中使用 **kAllUsers** 设置。

![阐释所有侦听器通知的关系图](images/notifyfilt2.gif)

下图显示了这样一种情况：用户1和用户2都注册了通知，方法是调用 **RegisterForPrintAsyncNotifications** 函数，并在调用中传递 **kPerUser** 枚举器。 对于发送的三个通知，侦听器用户1从会话0或会话1中的用户1接收通知。 侦听器用户2接收来自会话2中的用户2的通知。

![说明每用户筛选通知的关系图](images/notifyfilt3.gif)

如果上图中显示的侦听客户端调用了 **RegisterForPrintAsyncNotifications**，但这次在调用中传递 **kAllUsers** 枚举器，则所有会话中的所有侦听器都将收到三个通知。 请注意，只有管理员才能在对此函数的调用中使用 **kAllUsers** 枚举器。

## <a name="administrators"></a>管理员

管理员是具有 \_ \_ 指定打印对象的 "打印机访问" 管理权限的用户。 管理员可以向任何人发送通知，并可以接收任何人的通知。 请注意，仍将强制实施通知筛选器。

在下图中，Joe 使用 **kPerUser** 在通道上发送通知。 根据此枚举器对通道进行筛选时，通知只应发送到属于用户1的会话，即会话1。 但是，通知还会发送到会话2，因为有一个管理员正在侦听该通知并侦听此类型的通知。 请注意，会话3中的管理员不会收到通知，因为通知类型不相同。

![说明每用户和通知类型筛选的关系图](images/notifyfilt4.gif)

## <a name="specifying-the-type-of-communication"></a>指定通信类型

通过指定通信类型，打印组件将指示侦听器客户端是否需要响应，以及当从多个客户端发回通知时，后台处理程序处理此情况的方式。

```cpp
typedef enum
{
  kBidirectional = 1,
  kUnidirectional,
} PrintAsyncNotifyConversationStyle
```

有两种类型的通信：单向和双向。 在单向通信中，侦听客户端不响应后台处理程序通知。 在这种情况下，侦听客户端无法发送回通知，因为它收到 **空** 的 [IPrintAsyncNotifyChannel](/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifychannel)接口指针。 在双向通信中，客户端在收到通知时将发送响应，并在包含打印组件的对话框上携带。 这是 UI 通知的情况。

多个会话接收 UI 通知的情况值得注释。 在这种情况下，后台处理程序将打开一个通道，并通知与筛选器匹配的所有侦听器，并向它们发送第一个通知。 当第一个侦听器响应时，后台处理程序将关闭其他通道，并在第一个客户端继续对话。

如果管理员 (例如) 在注册的侦听客户端响应之前登录，则管理员将收到与侦听客户端相同的 UI 通知。

如果第一个用户 (管理员，例如) 发送响应，则后台处理程序会将与其他客户端的连接标记为 "已关闭"。 当其他侦听客户端最终响应时，它将收到 "通道已关闭" 消息。

## <a name="notification-types"></a>通知类型

通知类型是后台处理程序接受并用于筛选侦听器客户端的 GUID。  (参阅头文件 Prnasnot 中的 PrintAsyncNotificationType 类型定义。 ) 后台处理程序异步通知机制的任何客户端都可以定义自己的通知类型。 即使后台处理程序不知道发送的通知类型的意义，它仍将根据通知类型筛选侦听器客户端。

每个通知都必须与通知数据类型相关联。 此类型标识通知数据架构。

除了通知数据类型之外，还有一个与通道关联的类型，即通知通道类型。 通知发送方和侦听客户端出于不同目的使用通知通道类型。

在频道的发送方，当打印组件打开通道时，它可以指定它要通过该通道发送的通知类型。 通过该通道传递的所有通知都必须与通知通道类型属于同一类型。

发件人必须始终将某个类型与通知相关联，以便后台处理程序 "知道" 如何将其发送到相应的侦听客户端。 侦听客户端必须根据其自身的架构验证数据。 通知类型标识此架构。

在通道的侦听器端，侦听客户端可以通过在注册时指定某种通知数据类型来请求接收一种类型的通知。

后台处理程序定义一种特殊的通知类型，用于向侦听客户端通知服务或应用程序已终止。

```cpp
const GUID NOTIFICATION_RELEASE;
```

只有在调用 [IPrintAsyncNotifyCallback：： ChannelClosed](/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifycallback-channelclosed) 方法时，侦听客户端才能接收此类消息。

## <a name="notification-registration-handle"></a>通知注册句柄

当客户端注册通知时，服务器端后台处理程序将维护一个内部表，其中包含有关应用程序的信息，如其安全上下文。 通知注册句柄是客户端接收的不透明结构。

客户端只能通过使用此句柄注销来接收通知。

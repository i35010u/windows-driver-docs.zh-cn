---
title: 通知筛选和通信样式
description: 通知筛选和通信样式
ms.assetid: 66d019c2-0760-440d-acc4-85a7c073929a
keywords:
- 后台处理程序通知 WDK 打印筛选
- 打印后台处理程序通知 WDK，筛选
- 通知筛选 WDK 打印后台处理程序
- 筛选 WDK 后台处理程序通知
- CreatePrintAsyncNotifyChannel
- RegisterForPrintAsyncNotifications
- 通知数据类型 WDK 打印后台处理程序
- 数据类型 WDK 后台处理程序通知
- 通信 WDK 后台处理程序通知
- 所有侦听器通知 WDK 都打印后台处理程序
- 每个用户侦听器筛选 WDK 后台处理程序通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 400860734767a3aa137321575739e9204dd5743a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542302"
---
# <a name="notification-filtering-and-communication-styles"></a>通知筛选和通信样式





本部分介绍打印后台处理程序进程之间的接口组件，如打印处理器、 驱动程序和监视器。

### <a name="notification-filtering"></a>通知筛选

PrintAsyncNotifyUserFilter 枚举类型用于两种情况。 在其中第一个调用在后台处理程序内运行的打印组件[CreatePrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124750)函数来创建通知通道。 调用方传递 PrintAsyncNotifyUserFilter 枚举类型来指定哪些侦听客户端有权接收通知的一个枚举器。 在第二种情况下，侦听客户端调用[RegisterForPrintAsyncNotifications](https://go.microsoft.com/fwlink/p/?linkid=124752)函数来注册通知。 调用方传递一个 PrintAsyncNotifyUserFilter 枚举器，以指示它应接收的通知。

```cpp
typedef enum 
{
  kPerUser,
  kAllUsers
} PrintAsyncNotifyUserFilter; 
```

在图中， **kPerUser**调用中使用枚举器**CreatePrintAsyncNotifyChannel**函数。 因此，只有这两个侦听器运行中与用户相同的用户帐户进行注册的人有权接收通知。

![关系图演示如何筛选的每个用户侦听器](images/notifyfilt1.gif)

在下一步图中， **kAllUsers**调用中使用枚举器**CreatePrintAsyncNotifyChannel**函数。 因此，所有侦听器感兴趣的打印机或服务器可以都接收通知。 请注意只有管理员才有权使用**kAllUsers**中对此函数的调用设置。

![说明通知到的所有侦听器的关系图](images/notifyfilt2.gif)

下图显示了这种情况在其中用户 1 和用户 2 已注册的通知通过调用**RegisterForPrintAsyncNotifications**函数，传递**kPerUser**中的枚举器调用。 三个发送的通知，侦听器用户 1 从接收到通知用户 1 在会话 0 或会话 1 中。 侦听器用户 2 在会话 2 中接收来自用户 2 的通知。

![说明每个用户筛选的通知的关系图](images/notifyfilt3.gif)

如果已调用在上图中所示的侦听客户端**RegisterForPrintAsyncNotifications**，但此时间传递**kAllUsers**枚举器的调用中，所有会话中的所有侦听器将接收到三个通知。 请注意只有管理员才有权使用**kAllUsers**中对此函数的调用枚举器。

### <a href="" id="administrators-"></a>管理员

管理员是用户与打印机\_访问\_为指定的管理权限打印对象。 管理员可以向任何人发送通知，可以从任何人都收到通知。 请注意通知筛选器仍强制实施。

在下图中，Joe 发送通知的通道上**kPerUser**。 根据此枚举器筛选频道时, 应只对属于用户 1，即会话 1 的会话发送通知。 但是，也会发送通知到会话 2，因为存在侦听管理员和侦听此类型的通知。 请注意，会话 3 中的管理员未收到通知，因为通知类型不相同。

![说明每个用户和通知类型筛选的关系图](images/notifyfilt4.gif)

### <a name="specifying-the-type-of-communication"></a>指定类型的通信

通过指定的通信类型，打印组件指示是否从侦听器客户端预期响应，方法以及后台处理程序处理这种情况时重新从多个客户端发送通知。

```cpp
typedef enum 
{
  kBidirectional = 1, 
  kUnidirectional, 
} PrintAsyncNotifyConversationStyle
```

有两种类型的通信-单向和双向。 在单向通信中，侦听客户端不响应的后台处理程序通知。 在这种情况下，侦听客户端无法发送通知后，因为它接收**NULL**[IPrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124758)接口指针。 在双向通信中，客户端发送的响应时它将接收通知，并执行上一个对话框，其中打印组件。 这是 UI 通知情况。

这种情况中的多个会话接收 UI 通知需要注释。 在此情况下，后台处理程序打开通道并通知所有匹配筛选器，将它们发送第一次通知的侦听器。 第一个侦听器响应时，后台处理程序关闭其他通道和对话框中继续执行第一个客户端。

如果以管理员身份 （例如） 登录已注册侦听客户端响应之前，则管理员将收到同一 UI 通知作为侦听客户端。

当第一个用户 （例如，管理员） 发送响应时，后台处理程序会将标记与其他客户端连接为"已关闭"。 当其他侦听客户端最终做出响应时，它接收"通道已关闭"消息。

### <a name="notification-types"></a>通知类型

通知类型是一个 GUID，后台处理程序接受并使用来筛选侦听器客户端。 （请在头文件 Prnasnot.h PrintAsyncNotificationType 类型定义）。后台处理程序异步通知机制的任何客户端可以定义其自己的通知类型。 即使后台处理程序不知道的发送的通知类型的含义，它仍将筛选侦听器客户端的通知类型。

每个通知都必须具有与之关联的通知数据类型。 此类型可标识通知数据架构。

除了通知数据类型，没有关联的通道的通知通道类型的类型。 通知发件人和侦听客户端将用于不同目的的通知通道类型。

在通道的发送端，当打印组件打开一个通道，它可以指定它想要通过该通道发送的通知的类型。 通过该通道传递通知的所有必须的通知通道类型与相同的类型。

发件人必须始终将类型与关联通知，以便让后台处理程序"知道"如何将其发送到适当的侦听客户端。 侦听客户端必须验证根据其自己的架构的数据。 此架构标识的通知类型。

通道在侦听器端，侦听客户端可以请求通过指定某一通知数据类型，当它注册接收通知的一种类型。

后台处理程序定义用于宣布向侦听客户端的服务或应用程序发生故障的特殊的通知类型。

```cpp
const GUID NOTIFICATION_RELEASE;
```

侦听客户端可以接收此类消息仅当其[IPrintAsyncNotifyCallback::ChannelClosed](https://go.microsoft.com/fwlink/p/?linkid=124756)调用方法。

### <a href="" id="notification-registration-handle-"></a>通知注册句柄

当客户端注册通知时，服务器端的后台处理程序维护的应用程序，例如其安全上下文信息的内部表。 通知注册句柄是客户端收到的不透明结构。

客户端可以取消注册接收通知，只能通过使用此句柄。

 

 





---
title: 通知通道
description: 通知通道
ms.assetid: 3161342a-0737-4f3b-bb16-32d6949bceea
keywords:
- 后台处理程序通知 WDK 打印，通道
- 打印后台处理程序通知 WDK、 通道
- 通知通道 WDK 打印后台处理程序
- CreatePrintAsyncNotifyChannel
- 通道通知 WDK 打印后台处理程序
- 数据通道 WDK 后台处理程序通知
- IPrintAsyncNotifyChannel
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b7ee7af0e2306b9e27cd1964ee98a02b7e63799
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544579"
---
# <a name="notification-channel"></a>通知通道





本部分包含有关的信息[CreatePrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124750)函数和[IPrintAsyncNotifyChannel](https://go.microsoft.com/fwlink/p/?linkid=124758)接口。

```cpp
HRESULT
 CreatePrintAsyncNotifyChannel(
    IN LPCWSTR,
    IN PrintAsyncNotificationType*,
    IN PrintAsyncNotifyUserFilter,
    IN PrintAsyncNotifyConversationStyle,
    IN IPrintAsyncNotifyCallback*,
 OUT IPrintAsyncNotifyChannel**
    );
```

打印组件调用**CreatePrintAsyncNotifyChannel**函数来创建通知通道。 通道可以是每个打印机或每个服务器。

打印组件可以打开通知通道，仅当该组件加载的后台处理程序。 Winspool.drv 禁用此功能，如果调用方在运行应用程序-内而不是在后台处理程序服务。 例如，当应用程序加载驱动程序来执行呈现，调用**CreatePrintAsyncNotifyChannel**失败。 但是，如果后台处理程序服务加载驱动程序将成功相同的调用。

Spoolss.lib 提供此功能，使端口监视器可以打开通道。 可以调用的组件在后台处理程序内运行的和，链接到 Spoolss.lib **CreatePrintAsyncNotifyChannel**函数。 以下过程说明对此函数的调用中每个输入参数的用途。 该过程的第一步应用于此函数中的第一个参数，第二个步骤适用于第二个参数，依此类推。

若要创建通知通道，指定以下各项：

1.  服务器的打印机的名称。

2.  通知通道类型。 调用方可以指定通过此通道发送的通知的类型。

3.  用户筛选器。 调用方可以指定要接收通知，或者作为通知发送相同的用户或所有用户的用户。

4.  会话筛选器。 调用方必须指定这是单向还是双向通道。 若要将标记为单向通道，将设置的最后一个参数 (类型的**IPrintAsyncNotifyChannel**\*\*) 的**CreatePrintAsyncNotifyChannel**到**NULL**.

5.  **IPrintAsyncNotifyCallback**通知返回来自通道的另一端时要调用的接口。 这可以是**NULL**，如果调用方不希望接收响应。

当**CreatePrintAsyncNotifyChannel**返回时，第六个参数 (类型的**IPrintAsyncNotifyChannel**\*\*) 指向包含的地址的内存位置**IPrintAsyncNotifyChannel**对象。 此对象标识通道，并用于将通知发送并关闭通道。

### <a name="iprintasyncnotifychannel-interface"></a>IPrintAsyncNotifyChannel Interface

**IPrintAsyncNotifyChannel**接口标识一个通道，并用于将通知发送并关闭通道。 当打印组件调用**CreatePrintAsyncNotifyChannel**函数来提供公开的对象创建一个通知通道，后台处理程序服务响应**IPrintAsyncNotifyChannel**接口。

此接口继承自**IUnknown**接口，以便客户端的后台处理程序通知机制可以实现 COM 或 c + + 对象。 在下面的代码示例中的接口声明显示了此继承：

```cpp
#define INTERFACE IPrintAsyncNotifyChannel
DECLARE_INTERFACE_(IPrintAsyncNotifyChannel, IUnknown)
{
    STDMETHOD(QueryInterface)(
        THIS_ 
        REFIID riid, 
        void** ppvObj
        ) PURE;
 
    STDMETHOD_(ULONG, AddRef)(
        THIS
        ) PURE;
 
    STDMETHOD_(ULONG, Release)(
        THIS
        ) PURE;
 
    STDMETHOD(SendNotification)(
         THIS_
         IN IPrintAsyncNotifyDataObject*
         ) PURE;
 
    STDMETHOD(CloseChannel)(
         THIS_
         IN IPrintAsyncNotifyDataObject*
         ) PURE;
};
```

若要发送通知，发件人调用[IPrintAsyncNotifyChannel::SendNotification](https://go.microsoft.com/fwlink/p/?linkid=124760)方法。 发件人可以是任一打印组件打开通道并发送通知或侦听客户端必须对通知做出响应时。 此方法以异步方式执行操作。 当该方法返回成功代码时，后台处理程序会尝试将通知发送到侦听器。 但不能保证任何侦听器接收的通知。

若要关闭通道，发件人或侦听器可以调用[IPrintAsyncNotifyChannel::CloseChannel](https://go.microsoft.com/fwlink/p/?linkid=124759)方法。 调用方可以传入一条通知，提供了在通道关闭的原因，或者可以将传递**NULL**指针。 当通道关闭时，将放弃所有排队的通知。

必须要小心，在调用[版本](https://go.microsoft.com/fwlink/p/?linkid=98433)通道对象，因为它没有采用所有常规的 COM 编程固定条件。 应调用**发行**上**IPrintAsyncNotifyChannel**才会出现以下情况：

-   如果您调用[AddRef](https://go.microsoft.com/fwlink/p/?linkid=98432)显式，并将它必须通过调用匹配**发行**。

-   如果创建的通道为单向的并且必须调用**版本**收到作为输出参数的指针上一次。 应调用**版本**后尚未发送所需的通知和关闭通道。

-   如果您创建作为双向通道，您可能必须调用**版本**收到作为输出参数的指针上一次。 应调用**版本**仅当您执行一个或多项操作：
    -   在调用之前**发行**对于双向通道，您必须始终调用**CloseChannel**和接收成功结果。 您不能调用**发行**如果在调用**CloseChannel**将失败，因为通道可能已发布你的名义。
    -   您必须调用**发行**输入时**ChannelClosed**事件。 若要避免这种情况下，检查调用**CloseChannel**的失败，出现错误通道\_ALREADY\_已关闭。 无需调用**版本**在这种情况下，因为你的名义已释放通道。
    -   您必须调用**CloseChannel**，**发行**，或任何其他成员函数在通道上，如果你**ChannelClosed**回调函数完成运行。 在这种情况下，通道已被释放，因此任何进一步的调用可能会导致未定义的行为。 此限制可能会要求您的前台线程和回调对象之间的协调。
    -   您必须确保您的前台线程和回调对象协调对调用**CloseChannel**并**发行**。 前台线程和回调对象不能以调用**CloseChannel**如果另一个是要调用或完成后调用**发行**。 您可以通过使用实现这一限制[ **3&gt;interlockedcompareexchange&lt;3}** ](https://msdn.microsoft.com/library/windows/hardware/ff547853)例程。 如果不使用**3&gt;interlockedcompareexchange&lt;3}**，可能会导致未定义的行为。
-   如果您注册为在通道上的侦听器，则可以调用**CloseChannel** ，然后调用**发行**在你[IPrintAsyncNotifyCallback::OnEventNotify](https://go.microsoft.com/fwlink/p/?linkid=124757)回调若要结束的双向通信的函数。 但是，您必须调用**CloseChannel**或**发行**在你**ChannelClosed**回调。

如果满足以下条件之一，则必须调用**版本**。 如果您不能满足这些条件之一，您必须调用**版本**。

**请注意**  调用**发行**任何上述条件，但第一个调用的顺序下**AddRef**到常规 COM 异常显式编程模式。 **IPrintAsyncNotifyChannel**不同于在此情况下标准 COM 做法。

 

 

 





---
title: 通知通道
description: 通知通道
ms.assetid: 3161342a-0737-4f3b-bb16-32d6949bceea
keywords:
- 后台处理程序通知 WDK 打印，频道
- 打印后台处理程序通知 WDK，通道
- 通知通道 WDK 打印后台处理程序
- CreatePrintAsyncNotifyChannel
- 频道通知 WDK 打印后台处理程序
- 数据通道 WDK 后台处理程序通知
- IPrintAsyncNotifyChannel
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 32dc6d685879392047d34348109a263fc48c7af1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209523"
---
# <a name="notification-channel"></a>通知通道

本部分包含有关 [CreatePrintAsyncNotifyChannel](/windows/win32/api/prnasnot/nf-prnasnot-createprintasyncnotifychannel) 函数和 [IPrintAsyncNotifyChannel](/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifychannel) 接口的信息。

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

打印组件调用 **CreatePrintAsyncNotifyChannel** 函数来创建通知通道。 频道可以是每个打印机或每个服务器。

仅当后台处理程序加载组件时，打印组件才能打开通知通道。 如果调用方在应用程序（而不是在后台处理程序服务中）运行，winspool.drv 将禁用此功能。 例如，当应用程序加载要执行呈现的驱动程序时，对 **CreatePrintAsyncNotifyChannel** 的调用将失败。 但是，如果后台处理程序服务加载了驱动程序，则相同的调用将成功。

Spoolss 提供了此功能，以便端口监视器可以打开通道。 在后台处理程序和链接到 Spoolss 的组件中运行的组件可以调用 **CreatePrintAsyncNotifyChannel** 函数。 下面的过程说明调用此函数时每个输入参数的用途。 该过程的第一步适用于此函数中的第一个参数，第二个步骤适用于第二个参数，依此类推。

若要创建通知通道，请指定以下项：

1. 打印机或服务器的名称。

1. 通知通道类型。 调用方可以指定要通过此通道发送的通知的类型。

1. 用户筛选器。 调用方可以指定要接收通知的用户，无论是通知发件人的用户还是所有用户。

1. 会话筛选器。 调用方必须指定这是单向还是双向通道。 若要将通道标记为单向，请将 CreatePrintAsyncNotifyChannel**类型的** () 的最后一个参数设置 \* \* 为**NULL**。 **CreatePrintAsyncNotifyChannel**

1. 当通知从通道的另一端返回时要调用的 **IPrintAsyncNotifyCallback** 接口。 如果调用方不希望收到响应，则此值可以为 **NULL**。

当**CreatePrintAsyncNotifyChannel**返回时， **IPrintAsyncNotifyChannel**类型的第六个参数 (\* \*) 指向包含**IPrintAsyncNotifyChannel**对象地址的内存位置。 此对象标识通道，并用于发送通知和关闭通道。

## <a name="iprintasyncnotifychannel-interface"></a>IPrintAsyncNotifyChannel 接口

**IPrintAsyncNotifyChannel**接口标识信道并用于发送通知和关闭通道。 当打印组件调用 **CreatePrintAsyncNotifyChannel** 函数来创建通知通道时，后台处理程序服务将通过提供一个公开 **IPrintAsyncNotifyChannel** 接口的对象来做出响应。

此接口继承自 **IUnknown** 接口，以便后台处理程序通知机制的客户端可以实现 COM 或 c + + 对象。 下面的代码示例中的接口声明演示了此继承：

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

若要发送通知，发送程序将调用 [IPrintAsyncNotifyChannel：： SendNotification](/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifychannel-sendnotification) 方法。 发件人可以是打开通道的打印组件，并在必须响应通知时发送通知或侦听客户端。 此方法以异步方式进行。 当该方法返回成功代码时，后台处理程序将尝试将通知发送到侦听器。 但不能保证任何侦听器收到通知。

若要关闭通道，发送方或侦听器可以调用 [IPrintAsyncNotifyChannel：： CloseChannel](/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifychannel-closechannel) 方法。 调用方可以传入通知，该通知提供关闭通道或可以传递 **NULL** 指针的原因。 关闭通道后，将丢弃所有排队的通知。

必须小心调用通道对象上的 [Release](/windows/win32/api/unknwn/nf-unknwn-iunknown-release) ，因为它不遵循所有常规 COM 编程的固定条件。 仅当出现以下情况时，才应在**IPrintAsyncNotifyChannel**上调用**Release** ：

- 如果显式调用了 [AddRef](/windows/win32/api/unknwn/nf-unknwn-iunknown-addref) ，则必须将其与 **Release**调用匹配。

- 如果已创建通道作为单向通道，并且必须在收到的作为输出参数的指针上调用一次 **发布** 。 在发送所需通知并结束通道后，应调用 **发布** 。

- 如果已创建通道作为双向通道，则可能必须在收到作为输出参数的指针上一次调用 **发布** 。 仅当你执行以下一项或多项操作时，才应调用 **Release** ：

  - 在调用双向通道的 **Release** 之前，必须始终调用 **CloseChannel** 并收到成功结果。 如果对**CloseChannel**的调用失败，则不得调用**Release** ，因为该通道可能已代表您发布。

  - 输入**ChannelClosed**事件时，不得调用**Release** 。 若要避免这种情况，请检查对 **CloseChannel** 的调用失败，错误通道 \_ 已 \_ 关闭。 在这种情况下，您无需调用 **发布** ，因为已代表您释放了该频道。

  - 如果**ChannelClosed**回调函数已完成运行，则不得在通道上调用**CloseChannel**、 **Release**或任何其他成员函数。 在这种情况下，通道已被释放，因此任何其他调用可能会导致未定义的行为。 此限制可能需要在前台线程和回调对象之间进行协调。

  - 必须确保前台线程和回调对象协调对 **CloseChannel** 的调用并 **释放**。 如果其他线程要调用或已完成调用**Release**，则前台线程和回调对象将无法开始对**CloseChannel**的调用。 可以使用 [**InterlockedCompareExchange**](/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedcompareexchange) 例程实现此限制。 如果不使用 **InterlockedCompareExchange**，则可能会导致未定义的行为。

- 如果在通道上注册为侦听器，则可以调用**CloseChannel** ，然后调用[IPrintAsyncNotifyCallback：： OnEventNotify](/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifycallback-oneventnotify)回调函数中的**Release**来结束双向通信。 但是，不能在**ChannelClosed**回调中调用**CloseChannel**或**Release** 。

如果满足这些条件之一，则必须调用 **Release**。 如果不满足上述条件之一，则不得调用 **Release**。

> [!NOTE]
> 在上述任何情况下调用 **Release** ，但第一个条件是显式调用 **AddRef** ，这是一般 COM 编程模式的例外。 在这种情况下， **IPrintAsyncNotifyChannel**与标准 COM 实践不同。
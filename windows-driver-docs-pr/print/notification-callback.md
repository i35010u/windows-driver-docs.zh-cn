---
title: 通知回调
description: 通知回调
keywords:
- 后台处理程序通知 WDK 打印，回拨
- 打印后台处理程序通知 WDK，回调
- 通知回调 WDK 打印后台处理程序
- IPrintAsyncNotifyCallback
- 回调 WDK 后台处理程序通知
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2d11801c4bab6b550cad95bd08c58666d8bbdd03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807785"
---
# <a name="notification-callback"></a>通知回调

对接收通知感兴趣的任何打印组件或侦听应用程序都必须提供公开 [IPrintAsyncNotifyCallback](/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifycallback) 接口的对象。 此接口继承自 **IUnknown** ，以便后台处理程序通知机制的客户端可以实现 COM 或 c + + 对象。

侦听应用程序在注册接收通知时，必须提供指向 **IPrintAsyncNotifyCallback** 接口的指针。 如果通知发件人对响应感兴趣并创建双向通道，则通知发件人必须提供指向 **IPrintAsyncNotifyCallback** 接口的指针。

```cpp
#define INTERFACE IPrintAsyncNotifyCallback
DECLARE_INTERFACE_(IPrintAsyncNotifyCallback, IUnknown)
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

    STDMETHOD(OnEventNotify)(
         THIS_
 IN IPrintAsyncNotifyChannel*,
         IN IPrintAsyncNotifyDataObject*
         ) PURE;

 STDMETHOD(ChannelClosed)(
         THIS_
         IN IPrintAsyncNotifyChannel*,
         IN IPrintAsyncNotifyDataObject*
         ) PURE;
};
```

当从通道的一端发送通知时，后台处理程序服务会在通道的另一端调用 [IPrintAsyncNotifyCallback：： OnEventNotify](/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifycallback-oneventnotify) 方法来传送通知。

当在一端关闭通知通道时，后台处理程序服务将调用另一端的 [IPrintAsyncNotifyCallback：： ChannelClosed](/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifycallback-channelclosed) 方法，以通告通道已关闭。 结束通道的原因将作为通知传递。

如果服务器或侦听应用程序停止，则后台处理程序断开代码会检测到这种情况，并且仍处于活动状态的通道的 "仍处于活动状态" 将通过 **IPrintAsyncNotifyCallback：： ChannelClosed** 调用（其中传递了通知 \_ 发布消息）通知。

---
title: 通知回调
description: 通知回调
ms.assetid: cf884097-45a4-4ef3-8ebb-64c006838235
keywords:
- 后台处理程序通知 WDK 打印，回调
- 打印后台处理程序通知 WDK、 回调
- 通知回调 WDK 打印后台处理程序
- IPrintAsyncNotifyCallback
- 回调 WDK 后台处理程序通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e2a91ba3ad89ffd19c554853cf15ad49c68c46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382850"
---
# <a name="notification-callback"></a>通知回调





任何打印组件或侦听感兴趣接收通知的应用程序必须提供公开的对象[IPrintAsyncNotifyCallback](https://go.microsoft.com/fwlink/p/?linkid=124755)接口。 接口继承自**IUnknown** ，以便客户端的后台处理程序通知机制可以实现或者 COM 或C++对象。

侦听应用程序必须提供一个指向**IPrintAsyncNotifyCallback**接口时它会注册以接收通知。 通知发件人必须提供一个指向**IPrintAsyncNotifyCallback**如果感兴趣的响应，还会创建一个双向通道的接口。

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

当从一端的通道发送通知时，后台处理程序服务调用[IPrintAsyncNotifyCallback::OnEventNotify](https://go.microsoft.com/fwlink/p/?linkid=124757)来传递通知的通道另一端的方法。

在一个最终关闭时通知通道，后台处理程序服务调用[IPrintAsyncNotifyCallback::ChannelClosed](https://go.microsoft.com/fwlink/p/?linkid=124756)另一端地宣布在通道关闭的方法。 在通道关闭的原因是作为通知传递。

如果服务器或侦听应用程序出现故障，后台处理程序断开代码检测到这种情况，并通过通知通道，它仍处于活动状态"仍处于活动状态"结束**IPrintAsyncNotifyCallback::ChannelClosed**调用，在该通知\_发布的消息传递。

 

 





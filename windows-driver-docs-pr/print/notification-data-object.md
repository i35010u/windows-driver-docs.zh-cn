---
title: 通知数据对象
description: 通知数据对象
ms.assetid: 6ba8840d-a693-485c-81da-81205e511120
keywords:
- 后台处理程序通知 WDK 打印，数据对象
- 打印后台处理程序通知 WDK，数据对象
- 通知数据对象 WDK 打印后台处理程序
- IPrintAsyncNotifyDataObject
- 数据对象 WDK 后台处理程序通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eea6f5532c4baf19af9d3671658ea1662ab7e6a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568585"
---
# <a name="notification-data-object"></a>通知数据对象





通知数据处理作为对象公开[IPrintAsyncNotifyDataObject](https://go.microsoft.com/fwlink/p/?linkid=124761)接口。 后台处理程序通知管道的客户端可以定义自己的数据架构，并且可以来回发送任何数据类型。 但是，后台处理程序查询通知数据对象的一个字节\*指针、 数据和通知类型的长度。 通知类型是 GUID，如中所述[通知类型](notification-filtering-and-communication-styles.md#notification-types)。

```cpp
#define INTERFACE IPrintAsyncNotifyDataObject
DECLARE_INTERFACE_(IPrintAsyncNotifyDataObject, IUnknown)
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
 
    STDMETHOD(AcquireData)(
         THIS_
         OUT BYTE**,
         OUT ULONG*,
         OUT PrintAsyncNotificationType**
         ) PURE;
 
    STDMETHOD(ReleaseData)(
        THIS
        ) PURE;
};
```

通知发件人必须在包数据**IPrintAsyncNotifyDataObject**对象。 发件人必须实现[IUnknown](https://go.microsoft.com/fwlink/p/?linkid=124716)接口。

侦听客户端调用[IPrintAsyncNotifyDataObject::AcquireData](https://go.microsoft.com/fwlink/p/?linkid=124762)方法以获取通知数据、 通知数据，并通知类型的大小的原始指针。

侦听客户端的数据完成后，它必须调用[IPrintAsyncNotifyDataObject::ReleaseData](https://go.microsoft.com/fwlink/p/?linkid=124763)方法。 后台处理程序通知管道的客户端必须实现**IPrintAsyncNotifyDataObject**接口的方式，如果**IPrintAsyncNotifyDataObject::Release**方法之前调用**IPrintAsyncNotifyDataObject::ReleaseData**方法调用时，不释放的对象。 建议调用**IPrintAsyncNotifyDataObject::AcquireData**方法应递增对象的引用计数，并且调用**ReleaseData**方法应递减对象的引用计数。

后台处理程序定义了一个特殊的通知类型名为通知 GUID\_版本。 断开的代码时后台处理程序或侦听应用程序停止运行，通过调用宣布"仍处于活动状态"的通道的末尾[IPrintAsyncNotifyChannel::CloseChannel](https://go.microsoft.com/fwlink/p/?linkid=124759)方法。

调用**IPrintAsyncNotifyDataObject::AcquireData**针对此通知的方法返回与字节\*\*参数设置为**NULL**，ULONG\*参数设置为 0 和 GUID\*参数设置为通知\_版本。

 

 





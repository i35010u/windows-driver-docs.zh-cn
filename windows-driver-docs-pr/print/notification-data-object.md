---
title: 通知数据对象
description: 通知数据对象
keywords:
- 后台处理程序通知 WDK 打印，数据对象
- 打印后台处理程序通知 WDK，数据对象
- 通知数据对象 WDK 打印后台处理程序
- IPrintAsyncNotifyDataObject
- 数据对象 WDK 后台处理程序通知
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: a38b39e919c82ef13154ffc113b9c212ea7e3dc8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807771"
---
# <a name="notification-data-object"></a>通知数据对象

通知数据将作为公开 [IPrintAsyncNotifyDataObject](/windows/win32/api/prnasnot/nn-prnasnot-iprintasyncnotifydataobject) 接口的对象处理。 后台处理程序通知管道的客户端可以定义自己的数据架构，并可以来回发送任何数据类型。 但是，后台处理程序将在通知数据对象中查询字节 \* 指针、数据的长度和通知类型。 通知类型为 GUID，如 [通知类型](notification-filtering-and-communication-styles.md#notification-types)中所述。

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

通知发送方必须将数据打包到 **IPrintAsyncNotifyDataObject** 对象中。 发件人必须实现 [IUnknown](/windows/win32/api/unknwn/nn-unknwn-iunknown) 接口。

侦听客户端将调用 [IPrintAsyncNotifyDataObject：： AcquireData](/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifydataobject-acquiredata) 方法，以获取指向通知数据的原始指针、通知数据的大小和通知类型。

当侦听客户端处理完数据后，必须调用 [IPrintAsyncNotifyDataObject：： ReleaseData](/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifydataobject-releasedata) 方法。 如果调用 **IPrintAsyncNotifyDataObject：： ReleaseData** 方法之前调用 **IPrintAsyncNotifyDataObject：： Release** 方法，则后台处理程序通知管道的客户端必须实现 **IPrintAsyncNotifyDataObject** 接口，不会释放对象。 建议对 **IPrintAsyncNotifyDataObject：： AcquireData** 方法的调用应递增对象的引用计数，并且对 **ReleaseData** 方法的调用应递减对象的引用计数。

后台处理程序定义了一个名为 "通知版本" 的特殊通知类型 GUID \_ 。 当后台处理程序或侦听应用程序停止时，断开代码通过调用 [IPrintAsyncNotifyChannel：： CloseChannel](/windows/win32/api/prnasnot/nf-prnasnot-iprintasyncnotifychannel-closechannel) 方法公布通道的 "仍处于活动" 状态。

对于此通知，对 **IPrintAsyncNotifyDataObject：： AcquireData** 方法的调用将返回，其中 BYTE \* \* 参数设置为 **NULL**，ULONG \* 参数设置为0，GUID \* 参数设置为通知 \_ 版本。

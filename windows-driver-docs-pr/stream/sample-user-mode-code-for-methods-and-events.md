---
title: 方法和事件的示例用户模式代码
description: 方法和事件的示例用户模式代码
ms.assetid: 0d564eb7-8e81-43bd-b539-f1240b3a21de
keywords:
- 事件 WDK AVStream
- AVStream 事件 WDK
- 用户模式 KsProxy 插件示例 WDK AVStream
- 方法 WDK AVStream
- 自动化表 WDK AVStream
- 通知 WDK AVStream
- KsProxy 插件示例 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 286bd3e0f0c650b74b0b9d733c33d139a75a39fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827378"
---
# <a name="sample-user-mode-code-for-methods-and-events"></a>方法和事件的示例用户模式代码


本部分中的代码演示如何使用用户模式 KsProxy 插件中的方法和事件。

若要了解如何支持内核模式微型驱动程序中的属性、方法和事件，请参阅[定义自动化表](defining-automation-tables.md)。

提供支持给定方法的微型驱动程序后，可以通过从用户模式插件调用[**IKsControl：： KsMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksmethod)来调用该方法，如下面的代码示例中所示。

```cpp
PVOID MethodBuffer; // Your method arguments buffer
ULONG MethodBufferSize; // Your method buffer size

KSMETHOD Method;
ULONG BytesReturned;

Method.Set = KSMETHODSETID_MyMethodSet;
Method.Id = KSMETHOD_MyMethodId;
Method.Flags = KSMETHOD_TYPE_SEND;

HRESULT hr = 
pIKsControl -> KsMethod (
    &Method,
        sizeof (Method),
    MethodBuffer,
    &MethodBufferSize,
    &BytesReturned);
```

在内核模式下提供的自动化表中，可以使用[**KSMETHOD\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmethod_item) **标志**成员来指定该缓冲区是否可读/写，是否应进行映射或复制。

若要注册你在微型驱动程序中支持的事件，请使用以下用户模式代码示例。

```cpp
HANDLE EventHandle; // Your event handle.

KSEVENT Event;
KSEVENTDATA EventData;

Event.Set = KSEVENTSETID_MyEventSet;
Event.Id = KSEVENT_MyEventId;
Event.Flags = KSEVENT_TYPE_ENABLE;

EventData.NotificationType = KSEVENTF_EVENT_HANDLE;
EventData.EventHandle.Event = EventHandle;
EventData.EventHandle.Reserved [0] = 0;
EventData.EventHandle.Reserved [1] = 0;

ULONG BytesReturned;

HRESULT hr =
pIKsControl -> KsEvent (
    &Event,
        sizeof (Event),
    &EventData,
        sizeof (EventData),
    &BytesReturned);
```

在上面的示例中，通知将继续，直到微型驱动程序禁用该事件。 禁用事件。 调用[**IKsControl：： KsEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksevent)。 如果希望仅在第一次发生此事件时收到通知，请在**KSEVENT 中设置**\_ONESHOT\_类型。

如果你正在支持带有 USB 视频类扩展单元的事件，请参阅[支持带扩展单元的自动更新事件](supporting-autoupdate-events-with-extension-units.md)。

 

 





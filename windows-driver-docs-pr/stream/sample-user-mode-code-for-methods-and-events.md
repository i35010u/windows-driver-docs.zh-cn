---
title: 方法和事件的示例用户模式代码
description: 方法和事件的示例用户模式代码
ms.assetid: 0d564eb7-8e81-43bd-b539-f1240b3a21de
keywords:
- 事件 WDK AVStream
- AVStream 事件 WDK
- 用户模式下 KsProxy 插件示例 WDK AVStream
- WDK AVStream 方法
- 自动化表 WDK AVStream
- 通知 WDK AVStream
- KsProxy 插件示例 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95f77a448fe853cff2a5ad91638378da915b5afa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389205"
---
# <a name="sample-user-mode-code-for-methods-and-events"></a>方法和事件的示例用户模式代码


在本部分中的代码演示如何使用方法和用户模式下 KsProxy 插件中的事件。

若要了解如何在你的内核模式微型驱动程序中支持属性、 方法和事件，请参阅[定义自动化表](defining-automation-tables.md)。

提供了支持给定的方法的微型驱动程序后，可以调用该方法通过调用[ **IKsControl::KsMethod** ](https://msdn.microsoft.com/library/windows/hardware/ff559785)从用户模式插件，如下面的代码示例中所示。

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

在自动化表提供在内核模式下，你可以使用**标志**的成员[ **KSMETHOD\_项**](https://msdn.microsoft.com/library/windows/hardware/ff563420)指定缓冲区是否是读/写和是否应映射或复制。

若要注册你微型驱动程序中支持的事件，请使用下面的用户模式代码示例。

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

在上述示例中，通知继续，直到微型驱动程序禁用该事件。 若要禁用该事件。 调用[ **IKsControl::KsEvent**](https://msdn.microsoft.com/library/windows/hardware/ff559772)。 如果你想要通知只在首次发生此事件，设置 KSEVENT\_类型\_中的 ONESHOT **Event.Flags**。

如果支持 USB 视频类扩展单位的事件，请参阅[扩展单位支持自动更新事件](supporting-autoupdate-events-with-extension-units.md)。

 

 





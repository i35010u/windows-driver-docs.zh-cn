---
title: 同步取消和完成代码
description: 同步取消和完成代码
ms.assetid: 4c302fc5-cb14-46e5-80c8-8dbf62486905
keywords:
- 请求处理 WDK KMDF、 取消请求
- I/O 请求 WDK KMDF，取消
- 同步 WDK KMDF
- 完成 I/O 请求 WDK KMDF
- 请求处理 WDK KMDF，同步
- I/O 请求 WDK KMDF，同步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bbd7a7fc72fca3d137c1ab605be0779a18da0c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547453"
---
# <a name="synchronizing-cancel-and-completion-code"></a>同步取消和完成代码





如果您的驱动程序调用[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)或[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)发出 I/O 请求那里可取消，则可能会同步问题。 例如，您的驱动程序和设备可能会执行设备 I/O 操作以异步方式通过的方式[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)并[ *EvtInterruptDpc*](https://msdn.microsoft.com/library/windows/hardware/ff541721)回调函数，且两*EvtInterruptDpc*并[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)回调函数可能包含对的调用[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)。

该驱动程序必须调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)只有一次为完成或取消请求。 但是，如果[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)并[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)回调函数不相互同步，框架可以将其他执行时调用其中一个。

避免此问题是如果您的驱动程序使用框架的简单[自动同步](using-automatic-synchronization.md)，因为自动同步可确保一次一个地，将调用的回调函数。

如果您的驱动程序不使用框架的自动同步，它可以使用[framework 锁](using-framework-locks.md)同步取消和完成代码。

该驱动程序是否使用框架的自动同步，或提供其自己的同步，该驱动程序的[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)回调函数必须调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)来取消的请求。 在驱动程序[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)回调函数应调用[ **WdfRequestUnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff550035) ，如下所示：

```cpp
Status = WdfRequestUnmarkCancelable(Request);
if( Status != STATUS_CANCELLED ) {
    WdfRequestComplete(Request, RequestStatus);
    }
```

此代码可确保该驱动程序不会调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)来完成该请求，如果该驱动程序已调用它取消请求。

详细了解您的驱动程序必须遵循时的规则中，它将调用**WdfRequestUnmarkCancelable**，请参阅[ **WdfRequestUnmarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff550035)。

 

 






---
title: Windows 2000 的 GDI 事件服务
description: Windows 2000 的 GDI 事件服务
ms.assetid: bf7f2127-cd3e-430c-99fd-62c824394a57
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，GDI 事件服务
- GDI WDK Windows 2000 显示事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 570ba9e5fa8c5d4c457915ec109d14226e58b3d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326189"
---
# <a name="gdi-event-services-in-windows-2000"></a>Windows 2000 的 GDI 事件服务


## <span id="ddk_gdi_event_services_in_windows_2000_gg"></span><span id="DDK_GDI_EVENT_SERVICES_IN_WINDOWS_2000_GG"></span>


[GDI 事件服务](gdi-event-services.md)介绍 GDI 与事件相关的函数，显示驱动程序可用于同步的组。 这些与事件相关的函数被记录为仅可在 Microsoft Windows XP 及更高版本，但大多数都还在 Microsoft Windows 2000 中可用。 尽管大部分这些与事件相关的函数都可以在 Windows 2000 中，实现 Windows 2000 的驱动程序中使用它们不建议，因为这样的驱动程序无法使 Windows 2000 不可靠。

可在 Windows 2000 中的事件相关的函数中的操作类似 Windows 2000 在除 Windows XP 中一样[ **EngWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff565461)函数。 **EngWaitForSingleObject**实现在 Windows 2000 中的返回的 DWORD 值，而不是 Windows XP 实现返回 BOOL 值。 该 DWORD 值可以是下列值之一：

<span id="Zero"></span><span id="zero"></span><span id="ZERO"></span>Zero  
指示发生了以下操作之一：

-   在等待成功。 也就是说，指定的事件对象设置为终止状态。 调用的线程**EngWaitForSingleObject**可以恢复处理。

-   调用线程传递到一个无效的事件对象指针*pEvent*的参数**EngWaitForSingleObject**。

<span id="Any_nonzero_value"></span><span id="any_nonzero_value"></span><span id="ANY_NONZERO_VALUE"></span>任何非零值  
此值是一个 NTSTATUS 状态值，指示特定错误情况。 例如，状态\_超时指示出现超时。

**请注意**   [ **EngClearEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff564190)并[ **EngReadStateEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565001)函数在中不可用Windows 2000。

 

 

 






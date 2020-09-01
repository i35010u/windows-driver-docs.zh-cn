---
title: Windows 2000 的 GDI 事件服务
description: Windows 2000 的 GDI 事件服务
ms.assetid: bf7f2127-cd3e-430c-99fd-62c824394a57
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，GDI 事件服务
- GDI WDK Windows 2000 显示，事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a20bf9c0eeb99439c4b1f47b01399fe6b402868a
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065840"
---
# <a name="gdi-event-services-in-windows-2000"></a>Windows 2000 的 GDI 事件服务


## <span id="ddk_gdi_event_services_in_windows_2000_gg"></span><span id="DDK_GDI_EVENT_SERVICES_IN_WINDOWS_2000_GG"></span>


[Gdi 事件服务](gdi-event-services.md) 描述了显示驱动程序可用于同步的一组与 GDI 事件相关的函数。 尽管这些与事件相关的函数记录为仅在 Microsoft Windows XP 和更高版本中可用，但在 Microsoft Windows 2000 中也提供了这些函数。 尽管这些与事件相关的大部分功能在 Windows 2000 中都可用，但不建议在为 Windows 2000 实现的驱动程序中使用它们，因为这样的驱动程序可以使 Windows 2000 不可靠。

Windows 2000 中提供的与事件相关的函数在 Windows 2000 中的行为与在 windows 中的行为类似，但 [**EngWaitForSingleObject**](/windows/desktop/api/winddi/nf-winddi-engwaitforsingleobject) 函数除外。 Windows 2000 中的 **EngWaitForSingleObject** 实现返回 DWORD 值，而不是 windows XP 实现返回的布尔值。 此 DWORD 值可以是下列值之一：

<span id="Zero"></span><span id="zero"></span><span id="ZERO"></span>无  
指示发生了下列操作之一：

-   等待成功。 也就是说，指定的事件对象已设置为终止状态。 调用 **EngWaitForSingleObject** 的线程可以继续处理。

-   调用线程将无效的事件对象指针传递到**EngWaitForSingleObject**的*pEvent*参数。

<span id="Any_nonzero_value"></span><span id="any_nonzero_value"></span><span id="ANY_NONZERO_VALUE"></span>任何非零值  
此值是一个 NTSTATUS 状态值，指示特定的错误条件。 例如，状态 \_ 超时指示发生了超时。

**注意**   [**EngClearEvent**](/windows/desktop/api/winddi/nf-winddi-engclearevent)和[**EngReadStateEvent**](/windows/desktop/api/winddi/nf-winddi-engreadstateevent)函数在 Windows 2000 中不可用。

 

 


---
title: 示例内核模式驱动程序
description: 示例内核模式驱动程序
ms.assetid: 09d08e07-e991-458f-aedf-018a0dd20af5
keywords:
- 内核模式驱动程序 WDK，示例
- 示例驱动程序 WDK 内核模式
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0eb9b6ac42f87181a368358a603853eba95c3ee2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534131"
---
# <a name="sample-kernel-mode-drivers"></a>示例内核模式驱动程序

WDK 提供了各种示例内核模式驱动程序。 安装 WDK src 后\\常规子目录包含适用于所有内核模式驱动程序的示例驱动程序代码。 这些示例还维护联机。 这些示例包括：

[**toaster**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster/toastpkg)  
为符合的驱动程序的一组提供的示例代码[Windows 驱动程序模型](windows-driver-model.md)(WDM)。 此示例还包括示例安装软件。

[**KMDF HID 设备筛选器驱动程序**（ioctl 示例）](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly)  
演示如何驱动程序应支持 I/O 控制代码。

[**event**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/event)  
说明了内核模式驱动程序可以使用以通知应用程序的硬件事件，如果应用程序请求通知的方法。 一种方法使用[事件对象](event-objects.md)和其他依赖于[队列](queuing-and-dequeuing-irps.md)通知请求之前发生的事件。

[**cancel**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/cancel)  
演示如何使用[取消安全 IRP 队列](cancel-safe-irp-queues.md)。

[**tracedrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)  
演示如何使用[WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556204)。

其他子目录\\src 目录包含为各种类型的硬件的内核模式驱动程序的示例代码。

## <a name="see-also"></a>另请参阅

[Microsoft Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)GitHub 上

---
Description: 用于处理由 UCX 发送的 I/O 请求的主机控制器驱动程序的最佳做法。
title: 处理 USB 主控制器驱动程序中的 I/O 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e2837d698a81d8fa27820b7b5c62d168901217
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357030"
---
# <a name="handle-io-requests-in-a-usb-host-controller-driver"></a>处理 USB 主控制器驱动程序中的 I/O 请求


用于处理由 UCX 发送的 I/O 请求的主机控制器驱动程序的最佳做法。

跟踪已创建的 USB 总线上的设备的主机控制器驱动程序的所有终结点的 UCX。 由 UCX 首先处理中心驱动程序，或由另一个是 USB 设备堆栈中较高的驱动程序发送任何数据传输请求。 UCX 负责转发到正确的终结点队列的 framework 请求对象。 USB 请求块 (URB) 包含在请求中可能指定的终结点的句柄。 如果指定的终结点的句柄，则 UCX 检查相应的终结点之间存在的设备的终结点。 如果存在指定的终结点句柄，则该请求转发到终结点的队列。 如果找不到指定的终结点句柄，则请求将失败。 如果指定了不到句柄，则该请求是默认终结点，并 UCX 将请求转发到该设备的主机控制器驱动程序的默认终结点队列。

若要确保与现有的 USB 驱动程序的兼容性，主控制器必须符合以下要求时完成 URB 请求：

-  [**WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)必须在调度调用\_级别。
-   如果 URB 已传送到其 framework 队列和驱动程序已开始处理它以同步方式调用驱动程序的线程或 DPC，该请求应还完成同步。 请求必须在单独的 DPC，可通过调用安排上完成[ **WdfDpcEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff547148)。
-   类似于上述要求，在接收时[ **EVT_WDF_IO_QUEUE_IO_CANCELED_ON_QUEUE** ](https://msdn.microsoft.com/library/windows/hardware/ff541756)或[ **EVT_WDF_REQUEST_CANCEL** ](https://msdn.microsoft.com/library/windows/hardware/ff541817)，必须完成 URB 请求从调用线程不同 DPC 或 DPC，主机控制器驱动程序。 默认情况下，WDF 以同步方式完成队列已取消的请求。 该行为可能会导致问题的 URB 请求。 出于此原因，该驱动程序必须提供*EvtIoCanceledOnQueue*其 URB 队列的回调。

框架请求对象[ **IOCTL\_内部\_USB\_提交\_URB** ](https://msdn.microsoft.com/library/windows/hardware/ff537271)包含位于 URB **Parameters.Others.Arg1**的请求。 URB 状态时请求完成时，必须设置为任一 USBD\_状态\_成功，或指示失败性质的故障状态。 Usb.h 标头文件中定义的失败状态的值。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)  




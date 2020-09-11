---
description: 用于处理由 UCX 发送的 i/o 请求的主机控制器驱动程序的最佳实践。
title: 处理 USB 主控制器驱动程序中的 I/O 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e107cfb6fb16ee38dff4da1fbe73682b1aae9743
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010399"
---
# <a name="handle-io-requests-in-a-usb-host-controller-driver"></a>处理 USB 主控制器驱动程序中的 I/O 请求


用于处理由 UCX 发送的 i/o 请求的主机控制器驱动程序的最佳实践。

UCX 跟踪 USB 总线上设备的主机控制器驱动程序所创建的所有终结点。 集线器驱动程序发送的任何数据传输请求，或由 USB 设备堆栈中较高级别的驱动程序发送的任何数据都首先由 UCX 处理。 UCX 负责将框架请求对象转发到正确的终结点队列。  (包含在请求中的 URB) 的 USB 请求块可以指定终结点句柄。 如果指定了终结点句柄，UCX 将在设备的终结点中检查相应的终结点。 如果指定的终结点句柄存在，则会将请求转发到终结点的队列。 如果找不到指定的终结点句柄，则请求失败。 如果未指定句柄，则请求为默认终结点，UCX 将请求转发到该设备的主机控制器驱动程序的默认终结点队列。

若要确保与现有 USB 驱动程序兼容，在完成 URB 请求时，主机控制器必须符合以下要求：

-  [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)必须在调度级别调用 WdfRequestComplete \_ 。
-   如果 URB 已传递到其框架队列，并且驱动程序开始在调用驱动程序的线程或 DPC 上同步处理它，则请求也不应同步完成。 该请求必须在单独的 DPC 上完成，可以通过调用 [**WdfDpcEnqueue**](/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpcenqueue)来安排。
-   类似于前述要求，接收 [**EVT_WDF_IO_QUEUE_IO_CANCELED_ON_QUEUE**](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue) 或 [**EVT_WDF_REQUEST_CANCEL**](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)时，主机控制器驱动程序必须在单独的 dpc 上从调用线程或 DPC 完成 URB 请求。 默认情况下，WDF 以同步方式在队列上完成取消的请求。 此行为可能会导致 URB 请求出现问题。 出于此原因，驱动程序必须为其 URB 队列提供 *EvtIoCanceledOnQueue* 回调。

[**IOCTL \_ 内部 \_ USB \_ 提交 \_ URB**](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)的框架请求对象包含一个 URB，其中包含**参数. 请求的参数。** 请求完成后，URB 状态必须设置为 USBD \_ 状态 \_ 成功，或设置为指示故障性质的失败状态。 故障状态值在 usb .h 头文件中定义。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)
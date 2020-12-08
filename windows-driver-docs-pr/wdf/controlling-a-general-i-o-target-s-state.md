---
title: 控制常规 I/O 目标的状态
description: 控制常规 I/O 目标的状态
keywords:
- 一般 i/o 目标 WDK KMDF，州
- 已启动 i/o 目标状态 WDK KMDF
- 已停止 i/o 目标状态 WDK KMDF
- 已关闭，用于查询-删除状态 WDK KMDF
- 已关闭 i/o 目标状态 WDK KMDF
- 已删除 i/o 目标状态 WDK KMDF
- 本地 i/o 目标 WDK KMDF
- 远程 i/o 目标 WDK KMDF
- 停止 i/o 目标 WDK KMDF
- 重新启动 i/o 目标 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63072e32834afdc1286c48f3ec303d63798f1f47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829078"
---
# <a name="controlling-a-general-io-targets-state"></a>控制常规 I/O 目标的状态


可以将 i/o 目标对象可视化为具有两个入口： a 入口和外门。 当框架将请求传递给目标设备对象时，外接程序控制，而在入口中控制允许请求进入 i/o 目标的时间。

框架定义一般 i/o 目标的以下状态：

<a href="" id="started"></a>*首先*  
I/o 目标对象的两个入口都处于打开状态。 驱动程序可以将 i/o 请求发送到 i/o 目标队列，框架将请求传递给相应的驱动程序。

<a href="" id="stopped"></a>*停下*  
I/o 目标的输入处于打开状态，但已关闭入口。 框架停止向相应的驱动程序传递请求。 若要向 i/o 目标发送 i/o 请求，驱动程序必须在每个请求的 [**wdf \_ 请求 \_ 发送 \_ 选项**](/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options)结构中设置 **WDF \_ 请求 \_ 发送 \_ 选项 " \_ 忽略 \_ 目标 \_ 状态**" 或 " **wdf \_ 请求 \_ 发送 \_ 选项 \_ \_ \_** "。

<a href="" id="purged"></a>*清除*  
I/o 目标对象的两个入口都已关闭。 驱动程序无法向 i/o 目标发送 i/o 请求，除非它设置 **wdf \_ 请求 \_ 发送 \_ 选项 " \_ 忽略 \_ 目标 \_ 状态** " 或 " **WDF \_ 请求发送" 选项 " \_ \_ \_ 发送 \_ 并 \_ 忘记**"。 此外，该框架还会取消 i/o 目标对象的内部队列中未处理的请求。 从 KMDF 版本1.11 开始，此状态可用。

<a href="" id="closed-for-query-remove"></a>*已关闭以进行查询-删除*  
远程 i/o 目标已暂时关闭，因为可能很快会删除该目标的设备。

<a href="" id="closed"></a>*闭*  
I/o 目标已关闭，无法启动或停止。

<a href="" id="deleted"></a>*删除*  
已删除 i/o 目标的设备。

[**WDF \_ IO \_ TARGET \_ 状态**](/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)枚举定义表示这些状态的值。 驱动程序可以调用 [**WdfIoTargetGetState**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetgetstate) 来获取 i/o 目标的状态。

### <a name="local-io-target-states"></a>本地 i/o 目标状态

框架将自动打开并启动本地 i/o 目标。

如有必要，驱动程序可以调用 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) 来暂时停止本地 i/o 目标并调用 [**WdfIoTargetStart**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart) 将其重新启动。 例如，如果检测到临时错误情况，驱动程序可能会停止本地 i/o 目标，如果更正错误条件，则重新启动 i/o 目标。

在 KMDF 版本1.11 及更高版本中，驱动程序可以调用 [**WdfIoTargetPurge**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge) 来暂时阻止 i/o 请求发送到本地 i/o 目标，并取消目标队列中未处理的请求。 例如，在文件句柄清除过程中，驱动程序可能会清除本地 i/o 目标，以确保已取消发送到该驱动程序的所有请求。

如果删除了本地 i/o 目标设备，框架将自动停止并关闭 i/o 目标，并 [取消](canceling-i-o-requests.md) 目标队列中的所有 i/o 请求。 框架通过调用设备对象事件回调函数通知驱动程序设备不再可用。 有关这些回调函数的详细信息，请参阅 [PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

### <a name="remote-io-target-states"></a>远程 i/o 目标状态

驱动程序必须调用 [**WdfIoTargetOpen**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen) 以打开远程 i/o 目标。 当驱动程序打开远程 i/o 目标时，框架会自动启动 i/o 目标。

如有必要，驱动程序可以调用 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) 来暂时停止远程 i/o 目标并调用 [**WdfIoTargetStart**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart) 将其重新启动。

在 KMDF 版本1.11 及更高版本中，驱动程序可以调用 [**WdfIoTargetPurge**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge) 来暂时阻止 i/o 请求发送到远程 i/o 目标，并取消目标队列中未处理的请求。

如果删除了远程 i/o 目标设备，则框架将自动停止并关闭 i/o 目标，并取消目标队列中的所有 i/o 请求，除非驱动程序注册以下事件回调函数：

<a href="" id="evtiotargetqueryremove"></a>[*EvtIoTargetQueryRemove*](/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)  
通知驱动程序远程 i/o 目标设备可能已被删除。 如果希望驱动程序允许删除设备，则驱动程序必须调用 [**WdfIoTargetCloseForQueryRemove**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetcloseforqueryremove) 。

<a href="" id="evtiotargetremovecomplete"></a>[*EvtIoTargetRemoveComplete*](/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)  
通知驱动程序远程 i/o 目标的设备已被删除。 此回调函数必须调用 [**WdfIoTargetClose**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetclose)。

<a href="" id="evtiotargetremovecanceled"></a>[*EvtIoTargetRemoveCanceled*](/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)  
通知驱动程序删除远程 i/o 目标设备的尝试已被取消。 此回调函数必须调用 [**WdfIoTargetOpen**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)，驱动程序通常会调用 [**WDF \_ io \_ target \_ open \_ params \_ init \_ open**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_reopen) 来初始化其 WDF \_ io \_ target \_ open \_ params \_ init 函数。

如果驱动程序已经完成使用远程 i/o 目标并且不会再次使用目标，并且目标没有仍处于挂起状态的子请求对象，则驱动程序可以调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) ，而无需先调用 [**WdfIoTargetClose**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetclose)。 如果目标具有任何仍处于挂起状态的子请求对象，则驱动程序必须先调用 **WdfIoTargetClose** ，然后才能安全地调用 **WdfObjectDelete**。

 


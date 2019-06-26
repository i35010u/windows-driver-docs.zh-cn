---
title: 控制常规 I/O 目标的状态
description: 控制常规 I/O 目标的状态
ms.assetid: 37f756bf-b655-428e-b72c-f86c71f1a2db
keywords:
- 常规 I/O 面向 WDK KMDF，状态
- 已启动 I/O 目标状态 WDK KMDF
- 停止 I/O 目标状态 WDK KMDF
- 已关闭的查询删除状态 WDK KMDF
- 已关闭的 I/O 目标状态 WDK KMDF
- 已删除的 I/O 目标状态 WDK KMDF
- 本地 I/O 面向 WDK KMDF
- 远程 I/O 面向 WDK KMDF
- 正在停止 I/O 面向 WDK KMDF
- 重新启动 I/O 面向 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af29ae3c9eb6400341b03e91218e02eb157b8ac8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382873"
---
# <a name="controlling-a-general-io-targets-state"></a>控制常规 I/O 目标的状态


你可以为具有两个入口可视化 I/O 目标对象： 中入口和 out-gate。 当框架将请求传递到目标设备对象，而在入口控制请求允许的时间在所有输入的 I/O 目标 out-gate 的控件。

该框架定义常规 I/O 目标的以下的状态：

<a href="" id="started"></a>*已启动*  
这两个入口 I/O 目标对象处于打开状态。 驱动程序可以将 I/O 请求发送到 I/O 目标队列，并在 framework 将请求传递到相应的驱动程序。

<a href="" id="stopped"></a>*已停止*  
在入口中的 I/O 目标处于打开状态，但是 out-gate 已关闭。 该框架会停止将请求传递到相应的驱动程序。 若要将输入/输出请求发送到 I/O 目标，该驱动程序必须设置任一**WDF\_请求\_发送\_选项\_忽略\_目标\_状态**或**WDF\_请求\_发送\_选项\_发送\_AND\_忘记**在每个请求[ **WDF\_请求\_发送\_选项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_send_options)结构。

<a href="" id="purged"></a>*清除*  
关闭这两个入口 I/O 目标对象。 除非它会设置该驱动程序无法将输入/输出请求发送到 I/O 目标**WDF\_请求\_发送\_选项\_忽略\_目标\_状态**或**WDF\_请求\_发送\_选项\_发送\_AND\_忘记**。 此外，框架将取消 I/O 目标对象的内部队列中的未处理的请求。 此状态是 KMDF 1.11 版中的开始提供。

<a href="" id="closed-for-query-remove"></a>*已关闭的查询删除*  
远程 I/O 目标已暂时关闭，因为可能很快就会删除其设备。

<a href="" id="closed"></a>*关闭*  
I/O 目标已关闭，无法启动或停止。

<a href="" id="deleted"></a>*已删除*  
已删除 I/O 目标设备。

[ **WDF\_IO\_目标\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ne-wdfiotarget-_wdf_io_target_state)枚举定义表示这些状态的值。 您的驱动程序可以调用[ **WdfIoTargetGetState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetgetstate)若要获取的 I/O 目标状态。

### <a name="local-io-target-states"></a>本地 I/O 目标状态

框架会自动打开，并启动本地 I/O 目标。

如果有必要，则该驱动程序可以调用[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)若要暂时停止本地 I/O 目标和调用[ **WdfIoTargetStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)到重新启动它。 例如，驱动程序可能会停止本地 I/O 目标，如果它检测到临时错误条件，然后重新启动 I/O 目标，如果错误条件，则在更正。

KMDF 1.11 和更高版本，该驱动程序可以调用[ **WdfIoTargetPurge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge)若要暂时阻止 I/O 请求发送到本地的 I/O 目标，并取消目标的队列中的未处理的请求。 例如，文件句柄清理的一部分，驱动程序可能会清除本地的 I/O 目标，以确保所有请求都发送到驱动程序将被都取消。

如果移除本地 I/O 目标设备后，框架会自动停止并关闭 I/O 目标和[取消](canceling-i-o-requests.md)目标的队列中的所有 I/O 请求。 该框架会通知驱动程序，该设备不可再通过调用回调函数的设备对象事件。 有关这些回调函数的详细信息，请参阅[PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

### <a name="remote-io-target-states"></a>远程 I/O 目标状态

驱动程序必须调用[ **WdfIoTargetOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)若要打开远程 I/O 目标。 当驱动程序打开远程 I/O 目标时，框架会自动启动 I/O 目标。

如果有必要，则该驱动程序可以调用[ **WdfIoTargetStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)若要暂时停止远程 I/O 目标并调用[ **WdfIoTargetStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)到重新启动它。

KMDF 1.11 和更高版本，该驱动程序可以调用[ **WdfIoTargetPurge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetpurge)若要暂时阻止 I/O 请求发送到远程的 I/O 目标，并取消目标的队列中的未处理的请求.

如果移除远程 I/O 目标设备后，框架会自动停止和关闭 I/O 目标和取消的目标队列中的所有 I/O 请求，除非该驱动程序将注册以下事件回调函数：

<a href="" id="evtiotargetqueryremove"></a>[*EvtIoTargetQueryRemove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)  
告知驱动程序可能会删除远程 I/O 目标设备。 您的驱动程序必须调用[ **WdfIoTargetCloseForQueryRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetcloseforqueryremove)如果你想要允许删除该设备的驱动程序。

<a href="" id="evtiotargetremovecomplete"></a>[*EvtIoTargetRemoveComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_complete)  
告知驱动程序已删除远程 I/O 目标设备。 必须调用此回调函数[ **WdfIoTargetClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetclose)。

<a href="" id="evtiotargetremovecanceled"></a>[*EvtIoTargetRemoveCanceled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_remove_canceled)  
告知驱动程序已取消尝试删除远程 I/O 目标设备。 必须调用此回调函数[ **WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)，和驱动程序通常会调用[ **WDF\_IO\_目标\_打开\_PARAMS\_INIT\_重新打开**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_reopen)初始化其 WDF\_IO\_目标\_打开\_PARAMS\_INIT 函数。

如果驱动程序已完成使用远程 I/O 目标，且不会将目标，并且目标不包含任何子请求对象的仍是挂起状态，该驱动程序可以调用[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)而不必首先调用[ **WdfIoTargetClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetclose)。 如果目标具有任何子请求对象正在挂起、 驱动程序必须调用**WdfIoTargetClose**可以安全调用之前**WdfObjectDelete**。

 

 






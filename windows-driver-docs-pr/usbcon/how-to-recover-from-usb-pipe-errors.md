---
description: 本主题提供有关在将数据传输到 USB 管道失败时可尝试执行的步骤的信息。 本主题中所述的机制介绍了对批量、中断和同步管道的中止、重置和循环端口操作。
title: 如何从 USB 管道错误中恢复
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.custom: contperf-fy21q3
ms.openlocfilehash: a1fe04ff8486d3fd882f5588fdde95e46d52301f
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682228"
---
# <a name="how-to-recover-from-usb-pipe-errors"></a>如何从 USB 管道错误中恢复

> [!NOTE]
> 本文适用于设备驱动程序开发人员。 如果你在使用 USB 设备时遇到问题，请参阅 [排查常见 usb 问题](https://support.microsoft.com/windows/troubleshoot-common-usb-problems-5e9a9b49-ad43-702e-083e-6107e95deb88)

本主题提供有关在将数据传输到 USB 管道失败时可尝试执行的步骤的信息。 本主题中所述的机制介绍了对批量、中断和同步管道的中止、重置和循环端口操作。

USB 客户端驱动程序通过将控制传输发送到默认终结点来与其设备通信;数据传输到设备的批量、中断和同步终结点。 有时，这些传输可能会因各种原因而失败，例如终结点中的延迟情况。 如果传输失败，则关联的管道将无法处理请求，直到清除了错误条件。

对于控制传输，USB 驱动程序堆栈会自动清除错误条件。 对于数据传输，客户端必须采取适当的步骤从错误条件中进行恢复。 当数据传输失败时，USB 驱动程序堆栈会将错误报告给客户端驱动程序，USBD 状态代码失败。 根据状态代码，驱动程序可以提供错误恢复机制。

本主题提供有关通过这些操作进行的错误恢复的指导原则。

-   重置 USB 管道
-   重置设备连接到的 USB 端口
-   为客户端驱动程序循环 USB 端口以重新枚举设备堆栈

若要清除错误情况，请从重置管道操作开始，并根据需要执行更复杂的操作，例如重置端口和循环端口。

<em> ** *关于协调各种恢复机制</em>*： * *

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>客户端驱动程序必须协调不同的恢复操作，并确保在给定时间仅使用一种方法。 例如，请考虑一个具有两个终结点的设备：一个大容量和一个中断。 向设备发送几个数据传输请求之后，驱动程序会注意到请求在大容量管道上失败。 若要从这些错误中恢复，驱动程序会重置大容量管道。 但是，此操作不能解决传输错误，并且大容量传输会继续失败。 因此，驱动程序会发出用于重置 USB 端口的请求。 同时，传输在中断管道上开始失败，并随后进行重置设备请求。 若要从中断传输失败中恢复，驱动程序会在中断管道上发出重置管道请求。 如果这两个操作不协调，驱动程序可以同时启动两个重置设备操作，因为这两个管道上的故障。 同时进行的操作可能会出现问题。</p>
<p>客户端驱动程序必须确保在给定的时间，驱动程序只执行一个重置端口或循环端口操作。 在执行这些操作时，不应在任何管道上进行重置管道操作，驱动程序也不能发出新的重置管道请求。</p>
<p><em>Pankaj Gupta，Microsoft Windows USB 核心团队</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="what-you-need-to-know"></a>需要了解的事项


### <a name="technologies"></a>技术

-   [内核模式驱动程序框架](../wdf/index.md)

### <a name="prerequisites"></a>先决条件

-   客户端驱动程序必须已创建框架 USB 目标设备对象。

    如果使用 Microsoft Visual Studio Professional 2012 随附的 USB 模板，则模板代码会执行这些任务。 模板代码会获取目标设备对象的句柄并将其存储在设备上下文中。

    KMDF 客户端驱动程序必须调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) 方法来获取 WDFUSBDEVICE 句柄。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md) 中的“设备源代码”。

-   客户端驱动程序必须具有框架目标管道对象的句柄。 有关详细信息，请参阅 [如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

<a name="instructions"></a>说明
------------

### <a name="step-1-determine-the-cause-of-the-error-condition"></a><a href="" id="determine-the-cause-of-the-error-condition"></a>步骤1：确定错误情况的原因

客户端驱动程序通过使用 USB 请求块 (URB) 来启动数据传输。 请求完成后，USB 驱动程序堆栈返回一个 USBD 状态代码，指示传输是成功还是失败。 在失败的情况下，USBD 代码指示失败的原因。

-   如果通过调用 [**WdfUsbTargetDeviceSendUrbSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)方法提交了 URB，请在方法返回后检查 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的 "Hdr" 成员 **。**
-   如果通过调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 方法以异步方式提交 URB，请在 [*EVT_WDF_REQUEST_COMPLETION_ROUTINE*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)中检查 URB 状态。 *Params* 参数指向 [**WDF \_ 请求 \_ 完成 \_ 参数**](/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_completion_params)结构。 若要检查 USBD 状态代码，请检查 **&gt; UsbdStatus** 成员。 有关代码的信息，请参阅 [USBD \_ STATUS](/previous-versions/windows/hardware/drivers/ff539136(v=vs.85))。

传输故障可能由设备错误导致，如 \_ 检测到 USBD 状态 \_ 延迟 \_ PID 或 USBD \_ 状态 \_ 干扰 \_ 。 它们还可能是由于主机控制器报告了错误引起的，例如 USBD \_ 状态 \_ 事务 \_ 错误。

### <a name="step-2-determine-whether-the-device-is-connected-to-the-port"></a><a href="" id="determine-whether-the-device-is-connected-to-the-port"></a>步骤2：确定设备是否已连接到端口

发出重置管道或设备的任何请求之前，请确保设备已连接。 可以通过调用 [**WdfUsbTargetDeviceIsConnectedSynchronous**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceisconnectedsynchronous) 方法来确定设备的已连接状态。

### <a name="step-3-cancel-all-pending-transfers-to-the-pipe"></a><a href="" id="cancel-all-pending-transfers-to-the-pipe"></a>步骤3：取消到管道的所有待定传输

在发送重置管道或端口的任何请求之前，取消对管道的所有挂起的传输请求，即 USB 驱动程序堆栈尚未完成。 可以通过以下方式之一取消请求：

-   通过调用 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) 方法停止 i/o 目标。

    若要停止 i/o 目标，首先请通过调用 [**WdfUsbTargetPipeGetIoTarget**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetiotarget) 方法获取与框架管道对象关联的 WDFIOTARGET 句柄。 使用句柄调用 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)。 在调用中，将 "操作" 设置为 " **WdfIoTargetCancelSentIo** (参阅" [**WDF \_ io \_ 目标 \_ 发送 \_ io \_ 操作**](/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_sent_io_action) ") ，指示框架取消 USB 驱动程序堆栈尚未完成的所有请求。 对于已完成的请求，客户端驱动程序必须等待其完成回调，才能由框架调用。

-   发送中止管道请求。 可以通过调用以下方法之一发送请求：
    -   调用 [**WdfUsbTargetPipeAbortSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously) 方法。

        此调用是同步的，并且仅在取消所有挂起的请求后返回。 [**WdfUsbTargetPipeAbortSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously) 采用一个可选的 *请求* 参数。 建议将 WDFREQUEST 句柄传递到预分配的框架请求对象。 参数使框架可以使用指定的请求对象，而不是驱动程序无法访问的内部请求对象。 此参数值可确保 **WdfUsbTargetPipeAbortSynchronously** 不会由于内存不足而失败。

    -   调用 [**WdfUsbTargetPipeFormatRequestForAbort**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort) 方法，为中止管道请求设置请求对象的格式，然后通过调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 方法发送请求。

        如果驱动程序以异步方式发送请求，则它必须指定指向驱动程序实现的驱动程序 [*EVT_WDF_REQUEST_COMPLETION_ROUTINE*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine) 的指针。 若要指定指针，请调用 [**WdfRequestSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine) 方法。

        该驱动程序可以通过 \_ \_ 将 "WDF 请求发送 \_ 选项 \_ " 同步指定为 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)中的某个请求选项来同步发送请求。 如果同步发送请求，则改为调用 [**WdfUsbTargetPipeAbortSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously) 。

### <a name="step-4-reset-the-usb-pipe"></a><a href="" id="reset-the-usb-pipe"></a>步骤4：重置 USB 管道

通过重置管道开始恢复错误。 可以通过调用以下方法之一发送重置管道请求：

-   调用 [**WdfUsbTargetPipeResetSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpiperesetsynchronously) 以同步发送重置管道请求。
-   调用 [**WdfUsbTargetPipeFormatRequestForReset**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset) 方法为 reset 管道请求设置请求对象的格式，然后通过调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 方法发送该请求。 这些调用类似于中止管道请求，如步骤3中所述。

**注意**  请不要发送任何新的传输请求，直到重置管道操作完成。

 

重置管道请求会清除设备和主机控制器硬件中的错误条件。 若要清除设备错误，USB 驱动程序堆栈 \_ 使用终结点 \_ 暂停功能选择器向设备发送一个明确的功能控制请求。 请求的接收方是与管道关联的终结点。 如果错误条件发生在同步管道上，则驱动程序堆栈不会执行任何操作来清除设备，因为在发生错误的情况下，会自动清除同步终结点。

为了清除主机控制器错误，驱动程序堆栈会清除管道的暂停状态，并将管道的数据切换重置为0。

### <a name="step-5-reset-the-usb-port"></a><a href="" id="reset-the-usb-port"></a>步骤5：重置 USB 端口

如果重置管道操作未清除错误条件，并且数据传输继续失败，则发送重置端口请求。

1.  取消所有到设备的传输。 为此，请枚举当前配置中的所有管道，并取消为每个管道计划的挂起的请求。
2.  停止设备的 i/o 目标。

    调用 [**WdfUsbTargetDeviceGetIoTarget**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetiotarget) 方法以获取与框架目标设备对象关联的 WDFIOTARGET 句柄。 然后，调用 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) 并指定 WDFIOTARGET 句柄。 在 "调用" 中，将 "操作" 设置为 " **WdfIoTargetCancelSentIo** (WDF \_ io \_ 目标 \_ 发送 \_ IO \_ 操作") 。

3.  通过调用 [**WdfUsbTargetDeviceResetPortSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceresetportsynchronously) 方法发送重置端口请求。

重置端口操作导致设备在 USB 总线上重新枚举。 USB 驱动程序堆栈会在枚举之后保留设备配置。 由于驱动程序堆栈确保现有的管道句柄保持有效，因此客户端驱动程序可以使用以前获得的管道句柄。

不能重置复合设备的单个功能。 对于复合设备，当特定函数的客户端驱动程序发送重置端口请求时，整个设备将被重置。 如果 USB 设备维护状态，则重置端口请求可能会影响其他功能的客户端驱动程序。 因此，在重置端口前，客户端驱动程序会尝试重置管道。

### <a name="step-6-cycle-the-usb-port"></a><a href="" id="cycle-the-usb-port"></a>步骤6：循环 USB 端口

循环端口操作类似于拔出并插回端口的设备，不同的是设备未断开连接。 设备已断开连接并重新连接到软件。 此操作可导致设备重置和枚举。 因此，PnP 管理器将重新生成设备节点。

如果重置端口操作未清除错误条件，并且数据传输继续失败，则发送一个 "周期-端口请求"。

1.  取消所有到设备的传输。 请确保取消为当前配置中的每个管道计划的挂起请求 (参见步骤 3) 。
2.  停止设备的 i/o 目标。

    调用 [**WdfUsbTargetDeviceGetIoTarget**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetiotarget) 方法以获取与框架目标设备对象关联的 WDFIOTARGET 句柄。 然后，调用 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) 并指定 WDFIOTARGET 句柄。 在 "调用" 中，将 "操作" 设置为 " **WdfIoTargetCancelSentIo** (WDF \_ io \_ 目标 \_ 发送 \_ IO \_ 操作") 。

3.  通过调用以下方法之一发送循环端口请求：
    -   调用 [**WdfUsbTargetDeviceCyclePortSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecycleportsynchronously) 以同步发送循环端口请求。
    -   调用 [**WdfUsbTargetDeviceFormatRequestForCyclePort**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcycleport) 方法，为循环端口请求设置请求对象的格式，然后通过调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 方法发送请求。 这些调用类似于中止管道请求，如步骤3中所述。

只有在完成了 "周期-端口" 请求之后，客户端驱动程序才能将传输请求发送到设备。 这是因为当 USB 驱动程序堆栈处理循环端口请求时，设备节点会被删除。

循环端口请求会导致设备重新被枚举。 USB 驱动程序堆栈通知 PnP 管理器设备已断开连接。 与客户端驱动程序关联的 PnP 管理器泪水设备堆栈。 驱动程序堆栈重置设备，在 USB 总线上重新枚举设备，并通知 PnP 管理器设备已连接。 然后，PnP 管理器会为 USB 设备重新生成设备堆栈。

由于循环端口操作的原因，任何具有打开的句柄的应用程序都会获取设备删除通知， (如果为此类通知注册了应用程序) 。 作为响应，应用程序可能会向用户报告与设备断开连接的消息。 因为它会影响用户体验，所以，仅当其他恢复机制不能解决此错误情况时，客户端驱动程序才应选择使用循环端口请求。

与步骤 6) 中所述 (重置端口操作相似，对于复合设备，循环端口操作会影响整个设备，而不会影响设备的各个功能。

## <a name="related-topics"></a>相关主题
[USB i/o 传输](usb-device-i-o.md)
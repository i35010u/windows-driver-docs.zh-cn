---
Description: 本主题提供有关步骤的信息可以尝试在数据传输到 USB 管道时失败。 本主题涵盖中所述的机制中止，重置，并循环大容量、 中断，并等时管道上的端口操作。
title: 如何从 USB 管道错误中恢复
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8934d75986713bb65f32e461d388326a12304b9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364737"
---
# <a name="how-to-recover-from-usb-pipe-errors"></a>如何从 USB 管道错误中恢复


本主题提供有关步骤的信息可以尝试在数据传输到 USB 管道时失败。 本主题涵盖中所述的机制中止，重置，并循环大容量、 中断，并等时管道上的端口操作。

USB 客户端驱动程序通过将控件传输发送到默认终结点; 与其设备通信数据将传输到大容量、 中断和设备的同步终结点。 有时，这些传输可能会因各种原因，例如终结点中的停止条件失败。 如果传输失败，关联的管道无法处理请求，直到清除错误条件。

控制传输的 USB 驱动程序堆栈会自动清除错误条件。 对于数据传输，客户端必须采取适当措施来从错误情况中恢复。 当数据传输失败时，USB 驱动程序堆栈向通过失败 USBD 状态代码的客户端驱动程序报告错误。 根据状态代码，该驱动程序然后可以提供错误恢复机制。

本主题提供有关通过这些操作的错误恢复指南。

-   重置 USB 管道
-   重置设备连接的 USB 端口
-   循环要重新枚举设备的客户端驱动程序堆栈的 USB 端口

若要清除的错误条件，使用重置管道操作启动并执行更复杂的操作，例如重置端口和周期端口，仅当有必要。

<em>***有关协调各种恢复机制</em>*: * *

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>客户端驱动程序必须协调恢复的不同操作，并确保只有一个方法使用在给定的时间。 例如，考虑具有两个终结点的设备： 如果在大容量和中断。 后向设备发送少量数据传输请求，请求驱动程序通知失败在大容量管道上。 若要从这些错误中恢复，该驱动程序，重置批量管道。 但是，该操作不能解决的传输错误和大容量传输继续失败。 因此，该驱动程序发出请求以重置的 USB 端口。 同时，传输启动上中断管道，并随后重置设备请求失败。 若要从中断传输故障中恢复，该驱动程序发出中断管道上的重置管道请求。 如果这两项操作不协调，该驱动程序可以开始两个重置设备操作同时，由于这两个管道中出现故障。 这些并行操作可能存在问题。</p>
<p>客户端驱动程序必须确保，在给定时间，该驱动程序执行只需要一个重置端口或周期端口操作。 在这些期间，重置管道操作不应出现在任何管道上的进度和驱动程序必须发送新的重置管道请求。</p>
<p><em>Pankaj Gupta、 Microsoft Windows USB 核心团队</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="what-you-need-to-know"></a>你需要了解的内容


### <a name="technologies"></a>技术

-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>系统必备

-   客户端驱动程序必须已创建的 framework USB 目标设备对象。

    如果使用 Microsoft Visual Studio Professional 2012 使用提供的 USB 模板，模板代码执行这些任务。 模板代码获取目标设备对象的句柄，并将存储在设备上下文中。

    KMDF 客户端驱动程序必须通过调用获取 WDFUSBDEVICE 句柄[ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)方法。 详细信息，请参阅"设备源代码"中[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)。

-   客户端驱动程序必须具有框架目标管道对象的句柄。 有关详细信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

<a name="instructions"></a>说明
------------

### <a href="" id="determine-the-cause-of-the-error-condition"></a>步骤 1:确定错误条件的原因

客户端驱动程序通过使用 USB 请求块 (URB) 来启动数据传输。 在请求完成后，USB 驱动程序堆栈返回 USBD 状态代码指示传输是否成功还是失败。 在出现故障，USBD 代码指示失败的原因。

-   如果通过调用提交 URB [ **WdfUsbTargetDeviceSendUrbSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff550105)方法，检查**Hdr.Status**隶属[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构在方法返回之后。
-   如果你提交 URB 以异步方式通过调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)方法中，查看此 URB 状态[ *EVT_WDF_REQUEST_COMPLETION_ROUTINE*](https://msdn.microsoft.com/library/windows/hardware/ff540745). *Params*参数指向[ **WDF\_请求\_完成\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552454)结构。 若要检查 USBD 状态代码，检查**Usb-&gt;UsbdStatus**成员。 有关代码的信息，请参阅[USBD\_状态](https://msdn.microsoft.com/library/windows/hardware/ff539136)。

传输故障，可以得到与设备错误，例如 USBD\_状态\_停滞\_PID 或 USBD\_状态\_BABBLE\_检测到。 它们可能还会导致由于错误报告的主控制器，如 USBD\_状态\_XACT\_错误。

### <a href="" id="determine-whether-the-device-is-connected-to-the-port"></a>步骤 2:确定是否将设备连接到的端口

之前发出的任何请求都重置管道或设备，请确保设备已连接。 可以通过调用确定设备的连接的状态[ **WdfUsbTargetDeviceIsConnectedSynchronous** ](https://msdn.microsoft.com/library/windows/hardware/ff550095)方法。

### <a href="" id="cancel-all-pending-transfers-to-the-pipe"></a>步骤 3:取消所有挂起传输到管道

在发送前重置管道或端口的任何请求，取消所有挂起的转移请求管道，USB 驱动程序堆栈尚未完成。 您可以取消请求中通过以下方法之一：

-   通过调用停止 I/O 目标[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)方法。

    若要停止 I/O 目标，首先，获取通过调用与 framework 管道对象相关联的 WDFIOTARGET 句柄[ **WdfUsbTargetPipeGetIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff551146)方法。 通过使用该句柄，调用[ **WdfIoTargetStop**](https://msdn.microsoft.com/library/windows/hardware/ff548680)。 在调用中，将操作设置为**WdfIoTargetCancelSentIo** (请参阅[ **WDF\_IO\_目标\_SENT\_IO\_操作** ](https://msdn.microsoft.com/library/windows/hardware/ff552388)) 以指示框架将取消所有未完成的 USB 驱动程序堆栈的请求。 对于已完成的请求，客户端驱动程序必须等待其完成回调，若要获取由框架调用。

-   发送管道中止请求。 可以通过调用下列方法之一来发送请求：
    -   调用[ **WdfUsbTargetPipeAbortSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551129)方法。

        该调用为同步，并且返回仅所有挂起的请求将取消。 [**WdfUsbTargetPipeAbortSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551129)采用一个可选*请求*参数。 我们建议将 WDFREQUEST 句柄传递给预分配的 framework 请求对象。 参数允许使用的框架而不是一个内部请求对象，该驱动程序无法访问指定的请求对象。 此参数值可确保**WdfUsbTargetPipeAbortSynchronously**不会由于内存不足而失败。

    -   调用[ **WdfUsbTargetPipeFormatRequestForAbort** ](https://msdn.microsoft.com/library/windows/hardware/ff551132)方法设置格式的中止管道请求，请求对象，然后将请求发送通过调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)方法。

        如果驱动程序以异步方式发送请求，则它必须指定驱动程序的一个指向[ *EVT_WDF_REQUEST_COMPLETION_ROUTINE* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)驱动程序实现。 若要指定指针，调用[ **WdfRequestSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff550030)方法。

        驱动程序可以以同步方式发送请求，通过指定 WDF\_请求\_发送\_选项\_作为中的请求选项之一同步[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027). 如果以同步方式发送请求，然后调用[ **WdfUsbTargetPipeAbortSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551129)相反。

### <a href="" id="reset-the-usb-pipe"></a>步骤 4:重置 USB 管道

通过重置管道启动错误恢复。 可以通过调用下列方法之一发送重置管道请求：

-   调用[ **WdfUsbTargetPipeResetSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551156)以同步方式发送重置管道请求。
-   调用[ **WdfUsbTargetPipeFormatRequestForReset** ](https://msdn.microsoft.com/library/windows/hardware/ff551138)方法设置格式的重置管道请求中，一个请求对象，然后将请求发送通过调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)方法。 步骤 3 中所述，这些调用将类似于中止管道请求的。

**请注意**  不发送任何新转移请求，直到重置管道操作已完成。

 

重置管道请求清除设备和主机控制器硬件中的错误情况。 若要清除设备错误，USB 驱动程序堆栈发送明文\_到使用终结点设备功能控制请求\_HALT 功能选择器。 请求的接收方是与管道相关联的终结点。 如果同步管道上发生的错误条件，然后驱动程序堆栈不执行任何操作来清除设备，因为发生错误，会自动清除等时终结点。

若要清除主机控制器错误，驱动程序堆栈清除管道的停止状态，并将管道的数据切换按钮重置为 0。

### <a href="" id="reset-the-usb-port"></a>步骤 5:重置的 USB 端口

如果数据传输仍无法重置管道操作不会清除错误条件，将发送端口重置请求。

1.  取消所有传输到设备。 若要执行此操作，枚举中的当前配置的所有管道并取消挂起的请求，为每个管道计划。
2.  停止针对设备的 I/O。

    调用[ **WdfUsbTargetDeviceGetIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff550093)方法以获取与框架目标设备对象相关联的 WDFIOTARGET 句柄。 然后，调用[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)并指定 WDFIOTARGET 句柄。 在调用中，将操作设置为**WdfIoTargetCancelSentIo** (WDF\_IO\_目标\_SENT\_IO\_操作)。

3.  通过调用发送端口重置请求[ **WdfUsbTargetDeviceResetPortSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff550097)方法。

重置端口操作会导致设备重新获取枚举 USB 总线上。 USB 驱动程序堆栈保留后枚举的设备配置。 客户端驱动程序可以使用以前获得的管道句柄，因为驱动程序堆栈可确保现有管道句柄都保持有效。

无法重置复合设备的单个函数。 对于复合设备，当客户端驱动程序特定的函数的发送端口重置请求时，整个设备是重置。 如果 USB 设备维护状态，该重置端口请求可能会影响其他功能的客户端驱动程序。 因此，很重要，客户端驱动程序会尝试重置端口之前重置管道。

### <a href="" id="cycle-the-usb-port"></a>步骤 6:循环的 USB 端口

周期端口操作是类似于已断开并插入到端口，但采用未断开连接设备的设备。 设备已断开连接，并在软件中重新连接。 此操作会导致设备重置和枚举。 因此，即插即用管理器重新生成设备节点。

如果重置端口操作不会清除错误条件，数据传输仍无法发送周期端口请求。

1.  取消所有传输到设备。 请确保您取消挂起的请求的当前配置中每个管道计划 （请参阅步骤 3）。
2.  停止针对设备的 I/O。

    调用[ **WdfUsbTargetDeviceGetIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff550093)方法以获取与框架目标设备对象相关联的 WDFIOTARGET 句柄。 然后，调用[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)并指定 WDFIOTARGET 句柄。 在调用中，将操作设置为**WdfIoTargetCancelSentIo** (WDF\_IO\_目标\_SENT\_IO\_操作)。

3.  通过调用下列方法之一发送周期端口请求：
    -   调用[ **WdfUsbTargetDeviceCyclePortSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff550080)以同步方式发送周期端口的请求。
    -   调用[ **WdfUsbTargetDeviceFormatRequestForCyclePort** ](https://msdn.microsoft.com/library/windows/hardware/ff550084)方法设置格式对于周期端口的请求，请求对象，然后将请求发送通过调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)方法。 步骤 3 中所述，这些调用将类似于中止管道请求的。

仅在周期端口请求完成后，客户端驱动程序可以向设备发送传输请求。 这是因为 USB 驱动程序堆栈处理周期端口请求时，获取删除设备节点。

周期端口请求会导致设备重新获取枚举。 USB 驱动程序堆栈可以通知即插即用管理器已断开连接设备。 PnP 管理器终止与客户端驱动程序相关联的设备堆栈。 驱动程序堆栈重置设备、 重新枚举它在 USB 总线上并已连接的设备可以通知即插即用管理器。 PnP 管理器然后重新生成 USB 设备的设备堆栈。

为周期的端口操作，则有打开到设备的句柄的任何应用程序获取设备删除通知 （如果为此类通知注册应用程序）。 在响应中，应用程序可能会向用户报告设备断开连接消息。 因为它会影响用户体验，客户端驱动程序应该选择周期端口请求，仅当其他恢复机制不能解决的错误条件。

类似于重置端口操作 （在步骤 6 中所述），对于复合设备，周期端口操作会影响整个设备和设备的不是单个函数。

## <a name="related-topics"></a>相关主题
[USB I/O 传输](usb-device-i-o.md)  




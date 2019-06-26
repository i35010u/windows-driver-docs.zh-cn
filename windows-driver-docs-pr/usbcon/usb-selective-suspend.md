---
Description: 本部分提供有关选择正确的机制的选择性挂起功能的信息。
title: USB 选择性挂起
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33f661b9d2b4d406103a330c4dadf85478b7ce59
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356586"
---
# <a name="usb-selective-suspend"></a>USB 选择性挂起


本部分提供有关选择正确的机制的选择性挂起功能的信息。

在 Microsoft Windows XP 和更高版本操作系统，USB 核心 stack 支持的修改的版本"选择性挂起"功能时的通用串行总线规范中所述的修订版本 2.0。

USB 选择性挂起功能允许中心驱动程序，而不会影响中心上的其他端口操作挂起单个端口。 USB 设备的选择性挂起是便携式计算机中尤其有用，因为它可帮助节省电池电量。 很多设备，如指纹读取器和其他类型的生物识别扫描仪仅间歇性地要求能力。 当设备不在使用中，挂起此类设备，降低整体功率消耗。 更重要的是，不会有选择地挂起任何设备可能会阻止 USB 主控制器禁用其传输计划，将驻留在系统内存中。 DMA 传输由主机控制器到计划程序可以防止进入更深层次的睡眠状态，例如 C3 系统的处理器。 Windows 选择性挂起行为是不同的 Windows XP 和 Windows Vista 和更高版本的 Windows 中的设备。

有两种不同机制，用于有选择地挂起 USB 设备： 空闲请求 Irp ([**IOCTL\_内部\_USB\_提交\_空闲\_通知** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 并设置 power Irp ([**IRP\_MN\_设置\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power))。 要使用的机制取决于操作系统和设备类型： 复合或非复合。

##  <a name="selecting-a-selective-suspend-mechanism"></a>选择选择性挂起机制


客户端驱动程序，为复合设备上, 某个接口，使远程唤醒等的界面唤醒 IRP (IRP\_MN\_等待\_唤醒)，必须使用空闲请求 IRP ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 机制来有选择地挂起设备。

有关远程唤醒的信息，请参阅：

[远程唤醒的 USB 设备](https://docs.microsoft.com/windows-hardware/drivers/usbcon/remote-wakeup-of-usb-devices)

[等待/唤醒操作的概述](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-wait-wake-operation)

版本的 Windows 操作系统确定适用于非复合设备驱动程序的方式启用选择性挂起。

-   Windows XP:在 Windows XP 上所有客户端驱动程序必须使用空闲请求 Irp ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 关闭其设备的电源。 客户端驱动程序必须使用 WDM power Irp 来有选择地挂起其设备。 执行此操作将阻止其他设备有选择地挂起。 有关详细信息，请参阅"USB 全局挂起"。
-   Windows Vista 和更高版本的 Windows:驱动程序编写器已关闭设备在 Windows Vista 和更高版本的 Windows 中的多个选项。 尽管 Windows Vista 支持 Windows 空闲请求 IRP 机制，但驱动程序不需要使用它。

下表显示了需要使用空闲请求 IRP 的方案以及可以使用 WDM power IRP 挂起 USB 设备的：

| Windows 版本     | 在复合设备，能够了解唤醒函数 | 复合在设备上，不了解唤醒函数 | 单个接口 USB 设备 |
|---------------------|----------------------------------------------|--------------------------------------------------|-----------------------------|
| Windows 7           | 必须使用空闲请求 IRP                    | 可以使用 WDM Power IRP                            | 可以使用 WDM Power IRP       |
| Windows Server 2008 | 必须使用空闲请求 IRP                    | 可以使用 WDM Power IRP                            | 可以使用 WDM Power IRP       |
| Windows Vista       | 必须使用空闲请求 IRP                    | 可以使用 WDM Power IRP                            | 可以使用 WDM Power IRP       |
| Windows Server 2003 | 必须使用空闲请求 IRP                    | 必须使用空闲请求 IRP                        | 必须使用空闲请求 IRP   |
| Windows XP          | 必须使用空闲请求 IRP                    | 必须使用空闲请求 IRP                        | 必须使用空闲请求 IRP   |



本部分介绍 Windows 选择性挂起机制和包括以下主题：

# <a name="sending-a-usb-idle-request-irp"></a>将 USB 空闲请求 IRP 发送


当设备进入空闲状态时，客户端驱动程序将通知总线驱动程序来发送 IRP 的空闲状态请求 ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)). 总线驱动程序确定，则可以安全地将设备置于低功耗状态后，它会调用与空闲请求 IRP 堆栈的下层客户端设备驱动程序传递的回调例程。

在回调例程中，客户端驱动程序必须取消所有挂起 I/O 操作并等待所有 USB I/O Irp，才能完成。 它然后可以颁发[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求以更改到的 WDM 设备电源状态**D2**。 回调例程必须等待**D2**请求在返回之前完成。 有关空闲通知回调例程的详细信息，请参阅"USB 空闲通知回调例程"。

总线驱动程序不会调用发出的空闲通知回调例程后完成 IRP 空闲状态的请求。 相反，总线驱动程序保存空闲请求挂起的 IRP，直到满足以下条件之一成立：

-   **IRP\_MN\_SUPRISE\_删除**或**IRP\_MN\_删除\_设备 IRP**收到。 当收到这些 Irp 之一时空闲请求完成状态时 IRP\_已取消。
-   总线驱动程序收到的请求将设备放入工作电源状态 (**D0**)。 总线驱动程序在收到此请求时完成挂起空闲请求状态的 IRP\_成功。

以下限制适用于空闲请求 Irp 的使用：

-   驱动程序必须在设备电源状态下**D0**发送 IRP 的空闲请求时。
-   驱动程序必须将每个设备堆栈的只是一个空闲请求 IRP 发送。

下面的 WDM 示例代码说明了设备驱动程序将 USB 空闲请求 IRP 发送所需的步骤。 在下面的代码示例中的错误检查已被省略。

1.  分配并初始化[ **IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification) IRP
    ```cpp
    irp = IoAllocateIrp (DeviceContext->TopOfStackDeviceObject->StackSize, FALSE);
    nextStack = IoGetNextIrpStackLocation (irp);
    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_IDLE_NOTIFICATION;
    nextStack->Parameters.DeviceIoControl.InputBufferLength =
    sizeof(struct _USB_IDLE_CALLBACK_INFO);
    ```

2.  分配并初始化空闲请求信息结构 (USB\_空闲\_回调\_信息)。
    ```cpp
    idleCallbackInfo = ExAllocatePool (NonPagedPool,
    sizeof(struct _USB_IDLE_CALLBACK_INFO));
    idleCallbackInfo->IdleCallback = IdleNotificationCallback;
    // Put a pointer to the device extension in member IdleContext
    idleCallbackInfo->IdleContext = (PVOID) DeviceExtension;  
    nextStack->Parameters.DeviceIoControl.Type3InputBuffer =
    idleCallbackInfo;
    ```

3.  设置完成例程。

    客户端驱动程序必须将完成例程与空闲请求 IRP 相关联。 有关空闲通知完成例程和示例代码的详细信息，请参阅"USB 空闲请求 IRP 完成例程"。

    ```cpp
    IoSetCompletionRoutine (irp,
     IdleNotificationRequestComplete,
       DeviceContext,
       TRUE,
       TRUE,
       TRUE);

    ```

4.  空闲状态的请求存储在设备扩展。
    ```cpp
    deviceExtension->PendingIdleIrp = irp;

    ```

5.  发送到父驱动程序请求空闲。
    ```cpp
    ntStatus = IoCallDriver (DeviceContext->TopOfStackDeviceObject, irp);
    ```

## <a name="canceling-a-usb-idle-request"></a>正在取消 USB 空闲请求


在某些情况下，设备驱动程序可能需要取消的空闲状态的请求已提交到总线驱动程序的 IRP。 这可能是如果删除该设备，在空闲和空闲，发送请求后变为活动状态或如果整个系统正在过渡到较低的系统电源状态。

客户端驱动程序通过调用取消空闲 IRP [ **IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp)。 下表介绍用于取消空闲 IRP 的三种方案，并指定驱动程序的操作必须执行：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>应用场景</th>
<th>空闲请求取消机制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>客户端驱动程序已取消空闲的 IRP 和 USB 驱动程序堆栈不具有名为"USB 空闲通知回调例程"。</td>
<td><p>USB 驱动程序堆栈完成空闲 IRP。 因为设备永远不会离开<strong>D0</strong>，驱动程序不会更改设备状态。</p></td>
</tr>
<tr class="even">
<td>客户端驱动程序已取消空闲 IRP、 USB 驱动程序堆栈已调用 USB 空闲通知回调例程，和尚未返回。</td>
<td><p>很可能即使客户端驱动程序调用取消 IRP，调用 USB 空闲通知回调例程。 在这种情况下，客户端驱动程序的回调例程必须仍然关闭电源设备通过以同步方式将设备发送到低功率状态。</p>
<p>当设备处于较低的电源状态时，客户端驱动程序然后可以发送<strong>D0</strong>请求。</p>
<p>或者，驱动程序可以等待完成空闲 IRP，然后将发送的 USB 驱动程序堆栈<strong>D0</strong> IRP。</p>
<p>如果无法将设备置于低功耗状态由于内存不足，无法分配 power IRP 的回调例程，它应取消空闲 IRP 并立即退出。 将无法完成空闲 IRP，直到已返回回调例程;因此，回调例程不应阻止等待已取消的空闲 IRP 才能完成。</p></td>
</tr>
<tr class="odd">
<td>设备已处于低功耗状态。</td>
<td><p>如果设备已在低功耗状态中，客户端驱动程序可以发送<strong>D0</strong> IRP。 USB 驱动程序堆栈完成空闲请求与 STATUS_SUCCESS IRP。</p>
<p>或者，驱动程序可以取消空闲 IRP，等待 USB 驱动程序堆栈，以完成空闲 IRP，再然后发送<strong>D0</strong> IRP。</p></td>
</tr>
</tbody>
</table>

## <a name="usb-idle-request-irp-completion-routine"></a>USB 空闲请求 IRP 完成例程


在许多情况下，总线驱动程序可能会调用驱动程序的空闲请求 IRP 完成例程。 如果发生这种情况，客户端驱动程序必须检测总线驱动程序已完成 IRP 的原因。 返回的状态代码可以提供此信息。 如果状态代码不是状态\_电源\_状态\_无效，该驱动程序应将其设备放入**D0**如果设备已不在**D0**。 如果设备仍然空闲、 驱动程序可以提交另一个空闲请求 IRP。

**请注意**空闲请求 IRP 完成例程应不会阻止正在等待**D0** power 请求完成。 可以在完成例程 power IRP 的上下文中调用中心驱动程序，并完成例程中的另一个能力 IRP 上阻塞可能会导致死锁。

下面的列表指示空闲请求完成例程应如何解释一些常见的状态代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_SUCCESS</p></td>
<td><p>指示应不再挂起设备。 但是，驱动程序应该验证他们的设备提供支持，并将其放在<strong>D0</strong>如果它们尚不在<strong>D0</strong>。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_CANCELLED</p></td>
<td><p>总线驱动程序完成空闲请求 IRP 以便使用 STATUS_CANCELLED 任何以下情况中：</p>
<ul>
<li>设备驱动程序取消 IRP。</li>
<li>系统电源状态更改是必需的。</li>
<li>在 Windows XP 中，一个连接的 USB 设备的设备驱动程序无法将其设备放入<strong>D2</strong>时执行其空闲请求回调例程。 因此，总线驱动程序完成所有挂起的空闲请求 Irp。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>STATUS_POWER_STATE_INVALID</p></td>
<td><p>指示设备驱动程序请求<strong>D3</strong>电源状态为其设备。 当发生这种情况时，总线驱动程序中完成所有挂起的空闲 Irp STATUS_POWER_STATE_INVALID 使用。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_DEVICE_BUSY</p></td>
<td><p>指示总线驱动程序已保存的空闲请求挂起的 IRP 的设备。 只有一个空闲 IRP 可以处于挂起状态为给定设备一次。 提交多个空闲请求 Irp 电源策略所有者的部分错误，应处理由驱动程序编写器。</p></td>
</tr>
</tbody>
</table>



下面的代码示例显示了空闲请求完成例程的示例实现。

```ManagedCPlusPlus
/*Routine Description:

  Completion routine for idle notification IRP

Arguments:

    DeviceObject - pointer to device object
    Irp - I/O request packet
    DeviceExtension - pointer to device extension

Return Value:

    NT status value

--*/

NTSTATUS
IdleNotificationRequestComplete(
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp,
    IN PDEVICE_EXTENSION DeviceExtension
    )
{
    NTSTATUS                ntStatus;
    POWER_STATE             powerState;
    PUSB_IDLE_CALLBACK_INFO idleCallbackInfo;

    ntStatus = Irp->IoStatus.Status;

    if(!NT_SUCCESS(ntStatus) && ntStatus != STATUS_NOT_SUPPORTED) 
    {

        //Idle IRP completes with error.

        switch(ntStatus) 
        {

        case STATUS_INVALID_DEVICE_REQUEST:

            //Invalid request.

            break;

        case STATUS_CANCELLED:

            //1. The device driver canceled the IRP. 
            //2. A system power state change is required. 

            break;

        case STATUS_POWER_STATE_INVALID:

            // Device driver requested a D3 power state for its device
            // Release the allocated resources.

            goto IdleNotificationRequestComplete_Exit;

        case STATUS_DEVICE_BUSY:

            //The bus driver already holds an idle IRP pending for the device.

            break;

        default:
            break;

        }


        // If IRP completes with error, issue a SetD0

        //Increment the I/O count because
        //a new IRP is dispatched for the driver.
        //This call is not shown.

        powerState.DeviceState = PowerDeviceD0;

        // Issue a new IRP
        PoRequestPowerIrp (
            DeviceExtension->PhysicalDeviceObject, 
            IRP_MN_SET_POWER, 
            powerState, 
            (PREQUEST_POWER_COMPLETE) PoIrpCompletionFunc, 
            DeviceExtension, 
            NULL);
    }

IdleNotificationRequestComplete_Exit:

    idleCallbackInfo = DeviceExtension->IdleCallbackInfo;

    DeviceExtension->IdleCallbackInfo = NULL;

    DeviceExtension->PendingIdleIrp = NULL;

    InterlockedExchange(&DeviceExtension->IdleReqPend, 0);

    if(idleCallbackInfo)
    {
        ExFreePool(idleCallbackInfo);
    }

    DeviceExtension->IdleState = IdleComplete;

    // Because the IRP was created using IoAllocateIrp,
    // the IRP needs to be released by calling IoFreeIrp.
    // Also return STATUS_MORE_PROCESSING_REQUIRED so that
    // the kernel does not reference this.

    IoFreeIrp(Irp);

    KeSetEvent(&DeviceExtension->IdleIrpCompleteEvent, IO_NO_INCREMENT, FALSE);

    return STATUS_MORE_PROCESSING_REQUIRED;
}
```

## <a name="usb-idle-notification-callback-routine"></a>USB 空闲通知回调例程


总线驱动程序 （中心驱动程序的实例），或者泛型父驱动程序确定何时可以安全地挂起其设备的子级。 如果是，则会调用由每个孩子的客户端驱动程序提供的空闲通知回调例程。

USB 的函数原型\_空闲\_回调是按如下所示：

``` syntax
typedef VOID (*USB_IDLE_CALLBACK)(__in PVOID Context);
```

设备驱动程序必须在其空闲通知回调例程中执行以下操作：

-   请求[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP 如果设备需要了解有关远程唤醒设备。
-   取消所有 I/O 并准备好设备进入低功率状态。
-   通过调用将设备置于 WDM 睡眠状态中唤醒[ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)与*PowerState*参数设置为 PowerDeviceD2 （wdm.h 中; 中定义的枚举器值ntddk.h)。 在 Windows XP 中，驱动程序必须将放其设备 PowerDeviceD3，即使设备未配置为能够远程唤醒。

在 Windows XP 中，驱动程序必须依赖于要有选择地挂起设备发出的空闲通知回调例程。 如果在 Windows XP 中运行的驱动程序不使用空闲通知回调例程而直接将设备放入低功率状态，这可能会阻止 USB 设备树中的其他设备正在挂起。 有关更多详细信息，请参阅"USB 全局挂起"。

这两个中心驱动程序和[USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)发出的空闲通知回调例程调用在 IRQL = 被动\_级别。 这样，若要阻止等待电源状态更改请求完成时的回调例程。

仅当系统处于时调用回调例程**S0**并在设备处于**D0**。

以下限制适用于空闲请求通知回调例程：

-   设备驱动程序可以启动从一个设备电源状态转换**D0**到**D2**中发出的空闲通知回调例程，但没有其他电源允许状态转换。 具体而言，驱动程序必须不尝试更改到其设备**D0**时执行其回调例程。
-   设备驱动程序必须请求多个 power 从 IRP 内发出的空闲通知回调例程。

### <a name="arming-devices-for-wakeup-in-the-idle-notification-callback-routine"></a>武装的空闲通知回调例程中唤醒设备


空闲通知回调例程应确定其设备是否具有[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)请求挂起。 如果没有 IRP\_MN\_等待\_唤醒申请处于挂起状态，回调例程应提交 IRP\_MN\_等待\_之前挂起设备唤醒请求。 等待唤醒机制的详细信息，请参阅[支持的设备是否已唤醒功能](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)。


## <a name="usb-global-suspend"></a>USB 全局挂起


USB 2.0 规范定义全局挂起为整个总线背后 USB 主控制器的挂起的中止总线，包括开始帧的数据包上的所有 USB 流量。 尚未挂起的下游设备检测其上游端口上的空闲状态，并输入自己的挂起状态。 Windows 未实现全局挂起以这种方式。 它将停止在总线上的所有 USB 流量之前，Windows 始终有选择地挂起后 USB 主控制器的每个 USB 设备。

-   [条件全局在 Windows 7 中挂起](#conditions-for-global-suspend-in-windows-7)
-   [条件全局 Windows Vista 中挂起](#conditions-for-global-suspend-in-windows-vista)
-   [条件全局在 Windows XP 中挂起](#conditions-for-global-suspend-in-windows-xp)
-   [相关主题](#related-topics)

### <a name="conditions-for-global-suspend-in-windows-7"></a>条件全局在 Windows 7 中挂起


Windows 7 是更主动地有选择地挂起比 Windows Vista 的 USB 集线器。 Windows 7 USB 集线器驱动程序将有选择地挂起所有其连接的设备位于任何中心**D1**， **D2**，或**D3**设备电源状态。 整个总线将进入全局挂起所有 USB 集线器后选择性挂起。 Windows 7 USB 驱动程序堆栈将设备视为空闲只要设备处于 WDM 设备状态，就**D1**， **D2**，或**D3**。

### <a name="conditions-for-global-suspend-in-windows-vista"></a>条件全局 Windows Vista 中挂起


执行全局挂起的要求是在 Windows Vista 比 Windows XP 中更为灵活。

只要设备处于 WDM 设备状态的 USB 堆栈具体而言，将视为空闲 Windows Vista 中的设备**D1**， **D2**，或**D3**。

下图说明了在 Windows Vista 中可能出现的方案。

![windows vista 中挂起说明全局的关系图](images/global-suspendlh.png)

此图描述了与"条件适用于全局挂起在 Windows XP"的部分中所示的一个非常相似的情况。 但是，在这种情况下设备 3 限定为空闲状态的设备时。 由于所有设备都都处于空闲状态，总线驱动程序是可调用回调例程与挂起的空闲请求 Irp 相关联的空闲通知。 每个驱动程序挂起其设备，总线驱动程序挂起 USB 主控制器，只要它是安全地执行此操作。

在 Windows Vista 上所有非中心 USB 设备必须在**D1**， **D2**，或**D3**全局挂起将会启动之前，在这段时间所有 USB 集线器，包括根集线器，将都为挂起。 这意味着任何 USB 客户端驱动程序不支持选择性挂起，将阻止在总线输入全局挂起。

### <a name="conditions-for-global-suspend-in-windows-xp"></a>条件全局在 Windows XP 中挂起


为了最大限度地在 Windows XP 上的能源节约，十分重要，每个设备驱动程序使用空闲请求 Irp 挂起其设备。 如果一个驱动程序将使用其设备挂起[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求相反的空闲请求 IRP，它无法阻止其他设备正在挂起。

下图说明了在 Windows XP 中可能出现的方案。

![在 windows xp 中挂起说明全局的关系图](images/global-suspendxp.png)

在此图中，设备 3 电源状态下 D3 是，没有空闲 IRP 挂起的请求。 设备 3 没有资格用于全局空闲设备暂停使用在 Windows XP 中，因为它没有随其父级的空闲请求挂起的 IRP。 这可以防止总线驱动程序调用回调例程与树中的其他设备的驱动程序相关联的空闲状态的请求。

## <a name="enabling-selective-suspend"></a>启用选择性挂起


选择性挂起升级版本的 Microsoft Windows XP 已禁用。 它可用于 Windows XP、 Windows Vista 和更高版本的 Windows 的干净安装。

若要启用选择性挂起对给定的根中心和其子设备的支持，在选中的复选框**电源管理**USB 根集线器中的选项卡**设备管理器**。

或者，可以启用或禁用选择性暂停的值设置**HcDisableSelectiveSuspend** USB 端口驱动程序软件项下。 值为 1 禁用选择性挂起。 值为 0 允许选择性挂起。

例如，Usbport.inf 禁用选择性中的以下行挂起 Hydra OHCI 控制器：

```cpp
[OHCI_NOSS.AddReg.NT]
HKR,,"HcDisableSelectiveSuspend",0x00010001,1
```

客户端驱动程序不应尝试确定是否选择性挂起发送空闲请求之前已启用。 每当在设备处于空闲状态时，他们应提交空闲状态的请求。 如果空闲状态的请求失败，客户端驱动程序应重置空闲计时器，然后重试。

## <a name="related-topics"></a>相关主题
[USB 电源管理](usb-power-management.md)  




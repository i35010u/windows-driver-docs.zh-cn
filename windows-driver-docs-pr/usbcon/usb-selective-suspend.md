---
description: 本部分提供有关为选择性挂起功能选择正确机制的信息。
title: USB 选择性挂起
ms.date: 04/20/2017
ms.assetid: 828ee95a-7cfa-4905-acb8-5ae12acb0034
ms.localizationpriority: medium
ms.openlocfilehash: 57ff5db6b7270dfa180361ff85024cafec4d62bf
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968606"
---
# <a name="usb-selective-suspend"></a>USB 选择性挂起

本部分提供有关为选择性挂起功能选择正确机制的信息。

在 Microsoft Windows XP 和更高版本的操作系统中，USB 核心堆栈支持 "选择性挂起" 功能的修改版本，如通用串行总线规范的修订版2.0 中所述。

使用 USB 选择性挂起功能，集线器驱动程序可以挂起单个端口，而不会影响集线器上其他端口的操作。 USB 设备的选择性挂起在便携式计算机中特别有用，因为它有助于节省电池电量。 许多设备（如指纹读取器和其他类型的生物识别扫描器）只需要间歇地供电。 挂起此类设备，当设备未在使用时，会降低整体功率消耗。 更重要的是，任何未被选择性挂起的设备可能会阻止 USB 主机控制器禁用其传输计划，该计划驻留在系统内存中。 主机控制器向计划程序进行 DMA 传输会阻止系统的处理器进入更深层睡眠状态，例如 C3。 对于在 Windows XP 和 Windows Vista 及更高版本的 Windows 中运行的设备，Windows 选择性挂起行为有所不同。

有两种不同的机制可用于有选择地挂起 USB 设备：空闲请求 Irp ([**IOCTL \_ 内部 \_ usb \_ 提交 \_ 空闲 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 并设置电源 irp ([**IRP \_ MN \_ 设置 \_ 电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) 。 使用的机制取决于操作系统和设备类型：复合或非复合。

## <a name="selecting-a-selective-suspend-mechanism"></a>选择选择性挂起机制

客户端驱动程序（对于复合设备上的接口，该接口使用等待唤醒 IRP (IRP MN 等待唤醒) 启用远程唤醒的接口） \_ \_ \_ 必须使用空闲请求 IRP ([**IOCTL \_ 内部 \_ USB \_ 提交 \_ 空闲 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 机制，以便有选择地挂起设备。

有关远程唤醒的信息，请参阅：

[远程唤醒 USB 设备](https://docs.microsoft.com/windows-hardware/drivers/usbcon/remote-wakeup-of-usb-devices)

[等待/唤醒操作概述](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-wait-wake-operation)

Windows 操作系统的版本确定非复合设备的驱动程序启用选择性挂起的方式。

- Windows XP： Windows xp 上的所有客户端驱动程序都必须使用空闲请求 Irp ([**IOCTL \_ 内部 \_ USB \_ 提交 \_ 空闲 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 关闭其设备。 客户端驱动程序不得使用 WDM 电源 Irp 来有选择地挂起其设备。 这样做将阻止其他设备有选择地挂起。 有关详细信息，请参阅 "USB 全局挂起"。
- Windows Vista 和更高版本的 Windows：驱动程序编写器在 Windows Vista 和更高版本的 Windows 中提供了更多用于关闭设备的选项。 尽管 Windows Vista 支持 Windows idle 请求 IRP 机制，但驱动程序并不需要使用它。

下表显示了需要使用空闲请求 IRP 的方案，以及可以使用 WDM power IRP 来挂起 USB 设备的方案：

| Windows 版本     | 用于唤醒的合成设备上的函数 | 在复合设备上运行，不适用于唤醒 | 单接口 USB 设备 |
|---------------------|----------------------------------------------|--------------------------------------------------|-----------------------------|
| Windows 7           | 必须使用空闲请求 IRP                    | 可以使用 WDM Power IRP                            | 可以使用 WDM Power IRP       |
| Windows Server 2008 | 必须使用空闲请求 IRP                    | 可以使用 WDM Power IRP                            | 可以使用 WDM Power IRP       |
| Windows Vista       | 必须使用空闲请求 IRP                    | 可以使用 WDM Power IRP                            | 可以使用 WDM Power IRP       |
| Windows Server 2003 | 必须使用空闲请求 IRP                    | 必须使用空闲请求 IRP                        | 必须使用空闲请求 IRP   |
| Windows XP          | 必须使用空闲请求 IRP                    | 必须使用空闲请求 IRP                        | 必须使用空闲请求 IRP   |

本部分介绍 Windows 选择性挂起机制，并包括以下主题：

## <a name="sending-a-usb-idle-request-irp"></a>发送 USB 空闲请求 IRP

当设备进入空闲状态时，客户端驱动程序通过发送空闲请求 IRP ([**IOCTL \_ 内部 \_ USB \_ 提交 \_ 空闲 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 来通知总线驱动程序。 在总线驱动程序确定将设备置于低功耗状态后，它将调用回调例程，客户端设备驱动程序使用空闲请求 IRP 向下传递堆栈。

在回调例程中，客户端驱动程序必须取消所有挂起的 i/o 操作，并等待所有 USB i/o Irp 完成。 然后，它可以发出 [**IRP \_ MN \_ 设置 \_ 电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) 请求，将 WDM 设备电源状态更改为 **D2**。 回调例程必须等待 **D2** 请求完成后才返回。 有关空闲通知回调例程的详细信息，请参阅 "USB 空闲通知回调例程"。

在调用空闲通知回调例程后，总线驱动程序不会完成空闲请求 IRP。 相反，在满足以下条件之一之前，总线驱动程序会保持空闲请求 IRP 挂起：

- 已收到 **irp \_ MN \_ SUPRISE \_ 删除** 或 **irp \_ MN \_ REMOVE \_ DEVICE IRP** 。 如果收到其中一个 Irp，则空闲请求 IRP 完成，状态为 "已 \_ 取消"。
- 总线驱动程序会收到将设备置于工作电源状态 (**D0**) 的请求。 接收到此请求总线驱动程序完成挂起的空闲请求 IRP，状态为 " \_ 成功"。

以下限制适用于使用空闲请求 Irp：

- 发送空闲请求 IRP 时，驱动程序必须处于设备电源状态 **D0** 。
- 驱动程序必须为每个设备堆栈只发送一个空闲请求 IRP。

以下 WDM 示例代码说明了设备驱动程序发送 USB idle 请求 IRP 所需要执行的步骤。 下面的代码示例中省略了错误检查。

1. 分配并初始化 [**IOCTL \_ 内部 \_ USB \_ 提交 \_ 空闲 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification) IRP

    ```cpp
    irp = IoAllocateIrp (DeviceContext->TopOfStackDeviceObject->StackSize, FALSE);
    nextStack = IoGetNextIrpStackLocation (irp);
    nextStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
    nextStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_USB_SUBMIT_IDLE_NOTIFICATION;
    nextStack->Parameters.DeviceIoControl.InputBufferLength =
    sizeof(struct _USB_IDLE_CALLBACK_INFO);
    ```

2. 分配并初始化空闲请求信息结构 (USB \_ 空闲 \_ 回调信息 \_) 。

    ```cpp
    idleCallbackInfo = ExAllocatePool (NonPagedPool,
    sizeof(struct _USB_IDLE_CALLBACK_INFO));
    idleCallbackInfo->IdleCallback = IdleNotificationCallback;
    // Put a pointer to the device extension in member IdleContext
    idleCallbackInfo->IdleContext = (PVOID) DeviceExtension;  
    nextStack->Parameters.DeviceIoControl.Type3InputBuffer =
    idleCallbackInfo;
    ```

3. 设置完成例程。

    客户端驱动程序必须将完成例程与空闲请求 IRP 关联。 有关空闲通知完成例程和代码示例的详细信息，请参阅 "USB 空闲请求 IRP 完成例程"。

    ```cpp
    IoSetCompletionRoutine (irp,
        IdleNotificationRequestComplete,
        DeviceContext,
        TRUE,
        TRUE,
        TRUE);
    ```

4. 在设备扩展中存储空闲请求。

    ```cpp
    deviceExtension->PendingIdleIrp = irp;

    ```

5. 将空闲请求发送到父驱动程序。

    ```cpp
    ntStatus = IoCallDriver (DeviceContext->TopOfStackDeviceObject, irp);
    ```

## <a name="canceling-a-usb-idle-request"></a>取消 USB 空闲请求

在某些情况下，设备驱动程序可能需要取消已提交到总线驱动程序的空闲请求 IRP。 如果设备已被删除、处于空闲状态且发送了空闲请求，或者整个系统正在转换为较低系统电源状态，则可能会发生这种情况。

客户端驱动程序通过调用 [**IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)来取消空闲 IRP。 下表描述了用于取消空闲 IRP 并指定驱动程序必须执行的操作的三个方案：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>场景</th>
<th>空闲请求取消机制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>客户端驱动程序已取消空闲 IRP，并且 USB 驱动程序堆栈未调用 "USB 空闲通知回调例程"。</td>
<td><p>USB 驱动程序堆栈完成空闲 IRP。 由于设备从不会留下 <strong>D0</strong>，驱动程序不会更改设备状态。</p></td>
</tr>
<tr class="even">
<td>客户端驱动程序已取消空闲 IRP，USB 驱动程序堆栈调用了 USB 空闲通知回调例程，但尚未返回。</td>
<td><p>即使客户端驱动程序已在 IRP 上调用了取消，也可以调用 USB 空闲通知回调例程。 在这种情况下，客户端驱动程序的回调例程仍然必须通过以同步方式将设备发送到较低的电源状态关闭设备。</p>
<p>当设备处于低功耗状态时，客户端驱动程序可以发送 <strong>D0</strong> 请求。</p>
<p>或者，驱动程序可以等待 USB 驱动程序堆栈完成空闲 IRP，然后发送 <strong>D0</strong> irp。</p>
<p>如果由于内存不足而无法分配电源 IRP 来使设备进入低功耗状态，则应取消空闲 IRP 并立即退出。 在回调例程返回之前，不会完成空闲 IRP;因此，回调例程不应阻止等待已取消的空闲 IRP 完成。</p></td>
</tr>
<tr class="odd">
<td>设备已处于低功耗状态。</td>
<td><p>如果设备已处于低功耗状态，则客户端驱动程序可以发送 <strong>D0</strong> IRP。 USB 驱动程序堆栈完成空闲请求 IRP，并 STATUS_SUCCESS。</p>
<p>或者，驱动程序可以取消空闲 IRP，等待 USB 驱动程序堆栈完成空闲 IRP，然后发送 <strong>D0</strong> irp。</p></td>
</tr>
</tbody>
</table>

## <a name="usb-idle-request-irp-completion-routine"></a>USB 空闲请求 IRP 完成例程

在许多情况下，总线驱动程序可能会调用驱动程序的 "空闲请求 IRP 完成" 例程。 如果出现这种情况，客户端驱动程序必须检测到总线驱动程序完成 IRP 的原因。 返回的状态代码可以提供此信息。 如果状态代码不是状态 \_ "电源 \_ 状态 \_ 无效"，则驱动程序应将设备置于 **d0** 状态（如果设备尚未处于 **d0**状态）。 如果设备仍处于空闲状态，则驱动程序可以提交另一个空闲请求 IRP。

**注意**  空闲请求 IRP 完成例程不应阻止等待 **D0** 电源请求完成。 可以通过集线器驱动程序在 power IRP 的上下文中调用完成例程，并且在完成例程中的另一个电源 IRP 上阻塞可能会导致死锁。

以下列表说明了空闲请求的完成例程如何解释一些常见状态代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_SUCCESS</p></td>
<td><p>指示设备不应再挂起。 但是，驱动程序应该验证其设备是否已通电，如果它们尚未处于<strong>d0</strong>状态，请将其放入<strong>d0</strong> 。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_CANCELLED</p></td>
<td><p>总线驱动程序完成空闲请求 IRP，并在以下任一情况下 STATUS_CANCELLED：</p>
<ul>
<li>设备驱动程序已取消 IRP。</li>
<li>需要系统电源状态更改。</li>
<li>在 Windows XP 中，其中一个连接的 USB 设备的设备驱动程序在执行其空闲请求回调例程时无法将其设备放入 <strong>D2</strong> 。 因此，总线驱动程序完成所有挂起的空闲请求 Irp。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>STATUS_POWER_STATE_INVALID</p></td>
<td><p>指示设备驱动程序已为其设备请求 <strong>D3</strong> 电源状态。 发生这种情况时，总线驱动程序将完成所有挂起的空闲 Irp 并 STATUS_POWER_STATE_INVALID。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_DEVICE_BUSY</p></td>
<td><p>指示总线驱动程序已包含设备挂起的空闲请求 IRP。 对于给定设备，一次只能挂起一个空闲 IRP。 提交多个空闲请求 Irp 是电源策略所有者部分的错误，应由驱动程序编写器进行处理。</p></td>
</tr>
</tbody>
</table>

下面的代码示例演示了空闲请求完成例程的示例实现。

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

总线驱动程序 (集线器驱动程序或通用父驱动程序的实例) 确定何时可以安全地挂起其设备的子节点。 如果是，它将调用由每个子客户端驱动程序提供的空闲通知回调例程。

USB 空闲回调的函数原型如下所示 \_ \_ ：

``` syntax
typedef VOID (*USB_IDLE_CALLBACK)(__in PVOID Context);
```

设备驱动程序必须在其空闲通知回调例程中执行以下操作：

- 如果设备需要提供远程唤醒，请为设备请求 [**IRP \_ MN \_ 等待 \_ 唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP。
- 取消所有 i/o，并准备设备以降低电源状态。
- 通过调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) ，并将 PowerState 参数设置为枚举器值 PowerDeviceD2 (在*PowerState*中定义，使设备处于 WDM 睡眠状态;ntddk) 。 在 Windows XP 中，驱动程序不能将其设备放在 PowerDeviceD3 中，即使设备没有配备远程唤醒也是如此。

在 Windows XP 中，驱动程序必须依赖空闲通知回调例程来有选择地挂起设备。 如果在 Windows XP 中运行的驱动程序不使用空闲通知回调例程直接将设备置于低功耗状态，这可能会阻止 USB 设备树中的其他设备暂停。 有关更多详细信息，请参阅 "USB 全局挂起"。

集线器驱动程序和 [USB 泛型父驱动程序 ( # A0) ](usb-common-class-generic-parent-driver.md) 调用空闲通知回调例程，以 IRQL = 被动 \_ 级别。 这允许回调例程在等待电源状态更改请求完成时进行阻止。

仅当系统处于 **S0** 并且设备处于 **D0**中时，才调用回调例程。

以下限制适用于空闲请求通知回调例程：

- 设备驱动程序可以在空闲通知回调例程中启动从 **D0** 到 **D2** 的设备电源状态转换，但不允许进行其他电源状态转换。 具体而言，驱动程序在执行其回调例程时不能尝试将其设备更改为 **D0** 。
- 设备驱动程序不得从空闲通知回调例程内请求多个 power IRP。

### <a name="arming-devices-for-wakeup-in-the-idle-notification-callback-routine"></a>空闲通知回调例程中用于唤醒的武装设备

空闲通知回调例程应确定其设备是否已挂起 [**IRP \_ MN \_ 等待 \_ 唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) 请求。 如果没有任何 IRP \_ MN \_ 等待 \_ 唤醒请求处于挂起状态，则回调例程在 \_ 挂起设备之前应提交 IRP MN \_ wait \_ 唤醒请求。 有关等待唤醒机制的详细信息，请参阅 [支持具有唤醒功能的设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)。

## <a name="usb-global-suspend"></a>USB 全局挂起

USB 2.0 规范通过中止总线上的所有 USB 流量（包括框架起始数据包），将全局挂起定义为 USB 主机控制器后的整个总线暂停。 尚未挂起的下游设备会在其上游端口上检测到空闲状态，并自行进入挂起状态。 Windows 不会以这种方式实现全局挂起。 Windows 始终会有选择地挂起 USB 主机控制器后面的每个 USB 设备，然后它将停止总线上的所有 USB 流量。

- [Windows 7 中全局挂起的条件](#conditions-for-global-suspend-in-windows-7)
- [Windows Vista 中全局挂起的条件](#conditions-for-global-suspend-in-windows-vista)
- [Windows XP 中全局挂起的条件](#conditions-for-global-suspend-in-windows-xp)
- [相关主题](#related-topics)

### <a name="conditions-for-global-suspend-in-windows-7"></a>Windows 7 中全局挂起的条件

Windows 7 更积极地与 Windows Vista 一起暂停 USB 集线器。 Windows 7 USB 集线器驱动程序将有选择地挂起所有其附加设备处于 **D1**、 **D2**或 **D3** 设备电源状态的任何集线器。 所有 USB 集线器都处于选择性挂起状态后，整个总线将进入全局挂起。 每当设备处于 **D1**、 **D2**或 **D3**的 WDM 设备状态时，Windows 7 USB 驱动程序堆栈会将设备视为空闲。

### <a name="conditions-for-global-suspend-in-windows-vista"></a>Windows Vista 中全局挂起的条件

与 Windows XP 相比，在 Windows Vista 中执行全局挂起的要求更灵活。

特别是，每当设备处于 **D1**、 **D2**或 **D3**的 WDM 设备状态时，USB 堆栈会将设备视为处于空闲状态。

下图说明了 Windows Vista 中可能出现的情况。

![演示 windows vista 中的全局挂起的关系图](images/global-suspendlh.png)

此图说明了与 "在 Windows XP 中全局挂起的条件" 一节中描述的情况非常相似的情况。 但是，在这种情况下，设备3会限定为空闲设备。 由于所有设备都处于空闲状态，因此总线驱动程序能够调用与挂起的空闲请求 Irp 关联的空闲通知回调例程。 每个驱动程序会挂起其设备，并且总线驱动程序会在不安全的情况尽快暂停 USB 主机控制器。

在 Windows Vista 上，所有非集线器 USB 设备都必须位于 **D1**、 **D2**或 **D3** 中，然后才能启动全局挂起，此时所有 USB 集线器（包括根集线器）都将被挂起。 这意味着，任何不支持选择性挂起的 USB 客户端驱动程序都将阻止总线进入全局挂起状态。

### <a name="conditions-for-global-suspend-in-windows-xp"></a>Windows XP 中全局挂起的条件

为了最大限度地节省 Windows XP 的能耗，每个设备驱动程序都必须使用空闲请求 Irp 来挂起其设备，这一点非常重要。 如果一个驱动程序使用 [**IRP \_ MN \_ 设置 \_ 电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) 请求而不是空闲请求 IRP 来挂起其设备，则可能会阻止其他设备暂停。

下图说明了 Windows XP 中可能出现的情况。

![说明 windows xp 中全局挂起的关系图](images/global-suspendxp.png)

在此图中，设备3处于电源状态 D3，无空闲请求 IRP 处于挂起状态。 在 Windows XP 中，设备3不能作为一个空闲设备用于全局挂起，因为它没有挂起的空闲请求 IRP 及其父项。 这会阻止总线驱动程序调用与树中其他设备的驱动程序相关联的空闲请求回调例程。

## <a name="enabling-selective-suspend"></a>启用选择性挂起

为 Microsoft Windows XP 升级版本禁用了选择性挂起。 它用于 Windows XP、Windows Vista 和更高版本的 Windows 的全新安装。

若要为给定的根集线器及其子设备启用选择性挂起支持，请在**设备管理器**中选择 "USB 根集线器" 的 "**电源管理**" 选项卡上的复选框。

或者，你可以通过在 USB 端口驱动程序的软件密钥下设置 **HcDisableSelectiveSuspend** 的值来启用或禁用选择性挂起。 如果值为1，则禁用选择性挂起。 如果值为0，则启用选择性挂起。

例如，Usbport 中的以下行对 Hydra OHCI 控制器禁用选择性挂起：

```cpp
[OHCI_NOSS.AddReg.NT]
HKR,,"HcDisableSelectiveSuspend",0x00010001,1
```

在发送空闲请求之前，客户端驱动程序不应尝试确定是否启用了选择性挂起。 无论何时设备处于空闲状态，都应提交空闲请求。 如果空闲请求失败，客户端驱动程序应重置空闲计时器，然后重试。

## <a name="related-topics"></a>相关主题

[USB 电源管理](usb-power-management.md)  

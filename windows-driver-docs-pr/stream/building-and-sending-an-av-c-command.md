---
title: 生成和发送 AV/C 命令
description: 生成和发送 AV/C 命令
ms.assetid: 0f5bb205-7ffe-4007-bb66-a77889af2eed
keywords:
- Avc.sys 函数驱动程序 WDK、命令生成和发送
- 生成 WDK AV/C 的命令
- 发送 WDK AV/C 的命令
- AV/C WDK，命令
- Irp WDK AV/C
- I/O WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b0832800250d9de1fbcc63d91246e19b1742993
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107168"
---
# <a name="building-and-sending-an-avc-command"></a>生成和发送 AV/C 命令

以下过程概述了生成和发送 AV/C 命令的过程：

1. 子单位驱动程序必须分配和初始化一个 IRP，该 IRP 适用于其自身的驱动程序数 (如下面的驱动程序的设备 \_ 对象- &gt; **StackSize**成员) 中所指定的那样。 由驱动程序编写器实现的 IRP 管理样式会影响如何获取用于 *Avc.sys*的 irp。 通常，微型驱动程序调用 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 为 AV/C 命令分配新的 IRP。 不要在**IoAllocateIrp**的子单元驱动程序中分配的 IRP 上调用[**IoInitializeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp) 。 不要尝试重新初始化和重用旧的 IRP，而是在现有 IRP 上调用 [**IoFreeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp) ，然后调用 **IoAllocateIrp** 来分配新的 irp。

    > [!NOTE]
    > 为方便起见，下面的代码示例不演示错误处理。

    ```cpp
    PIRP Irp;
    Irp = IoAllocateIrp(DeviceExtension->ParentDeviceObject->StackSize, FALSE);
    ```

2. 然后，次级驱动程序分配一个 AVC \_ 命令 \_ IRB 或 AVC \_ MULTIFUNC \_ IRB 结构，该结构适用于所需的 av/c 函数类型，并使用所需的 av/c 请求参数填充块。 每个 IOCTL AVC 类函数的 "引用" 页 \_ \_ 描述了该函数所需的 IRB。 IRB 是一个数据块，用于描述要执行的 AV/C 操作码和操作。 *Avc.sys*支持的每个函数都与特定的 IRB 结构相关联。 必须从非分页池分配 IRB 的内存。 分配 IRB 的内存后，根据函数的关联结构定义填写函数的参数。

    有关可用函数及其关联结构定义的列表，请参阅 [av/c 协议驱动程序函数代码](./av-c-protocol-driver-function-codes.md)、 [Av/c 结构](/windows-hardware/drivers/ddi/_stream/index)和 [av/c 枚举](/windows-hardware/drivers/ddi/_stream/index)。

    下面的代码示例演示了如何 \_ \_ 为包含单个操作数字节的 AV/C 控制命令分配和初始化 AVC 命令 IRB 结构：

    ```cpp
    #include <avc.h>
    ...
    /* Define a custom pool tag to identify your subunit driver's memory allocations */
    #define CUSTOM_DRIVER_POOL_TAG 'C/VA'
    ...
    PAVC_COMMAND_IRB  AvcIrb;
    ...
    AvcIrb = ExAllocatePoolWithTag(NonPagedPool, sizeof(AVC_COMMAND_IRB), CUSTOM_DRIVER_POOL_TAG);
    ...
    RtlZeroMemory(AvcIrb, sizeof(AVC_COMMAND_IRB));

    #ifdef __cplusplus
    AvcIrb->Common.Function = AVC_FUNCTION_COMMAND;
    #else
    AvcIrb->Function = AVC_FUNCTION_COMMAND;
    #endif

    /*++ Do this to override the default time-out and retry values
    AvcIrb->TimeoutFlag = 1;
    AvcIrb->RetryFlag = 1;
    AvcIrb->Timeout.Quadpart = DEFAULT_AVC_TIMEOUT * 5;
    AvcIrb->Retries = 1;
    --*/
    AvcIrb->CommandType = AVC_CTYPE_CONTROL;
    AvcIrb->Opcode = Opcode;
    AvcIrb->OperandLength = 1;
    AvcIrb->Operand[0] = Operand;
    ```

3. 子单位驱动程序必须指定 IRP 的 **MajorFunction** 和 **DeviceIoControl IoControlCode** 成员，以及指向在步骤2中分配的 IRB 的指针。 在从操作系统分配 IRP 后，为相应的 IRB 分配非分页内存，然后设置 IRB 的参数，必须将 IRB 与 IRP 关联。 根据 IRB 的函数代码，必须在 IRP 中指定正确的调度例程。 对于与 IOCTL AVC 类对应的 AV/C 函数代码 \_ \_ (即， **DeviceIoControl. IoControlCode** 成员设置为 ioctl \_ AVC \_ CLASS) ，则 \_ \_ 必须将 IRP MN 内部 \_ 设备 \_ 控制指定为分配的 IRP 的 **MajorFunction** 值。 *Avc.sys*支持的所有其他 AV/C 函数代码（如[**ioctl \_ AVC \_ 更新 \_ 虚拟 \_ \_ **](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_update_virtual_subunit_info)子单位信息、 [**ioctl \_ AVC \_ 删除 \_ 虚拟 \_ \_ **](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_remove_virtual_subunit_info)子单位信息和[**IOCTL \_ AVC \_ 总线 \_ 重置**](/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_bus_reset)）都必须 \_ 将 IRP MJ \_ 设备控制指定 \_ 为分配的 irp 的**MajorFunction**值。

    下面的代码示例演示如何设置 IRP 以便 *Avc.sys* 进行处理：

    ```cpp
    #include <avc.h>
    ...
    PAVC_COMMAND_IRB  AvcIrb;
    PIRP Irp;
    PIO_STACK_LOCATION NextIrpStack;
    ...
    AvcIrb = ExAllocatePoolWithTag(NonPagedPool, sizeof(AVC_COMMAND_IRB), 'C/VA');
    ...
    Irp = IoAllocateIrp(DeviceExtension->ParentDeviceObject->StackSize, FALSE);
    ...
    NextIrpStack = IoGetNextIrpStackLocation(Irp);
    NextIrpStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
    NextIrpStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_AVC_CLASS;
    NextIrpStack->Parameters.Others.Argument1 = AvcIrb;
    ```

4. 子单位驱动程序必须至少为 IRP 指定一个 i/o 完成例程，该例程至少会分析响应。 完成例程还可以释放之前为未同步完成的 Irp 分配的 IRP 和 IRB 资源 (也就是说，如果 IRP 已标记为 "挂起" 之前) ，则完成例程仅释放 IRP 和 IRB 资源。

    需要 i/o 完成例程，因为子单位驱动程序必须分配 Irp 才能与 *Avc.sys*通信。 完成例程会阻止 i/o 管理器继续处理子源驱动程序的已分配 IRP，然后再调用该驱动程序的下部驱动程序完成。 I/o 完成例程必须始终返回状态 " \_ \_ 需要的更多处理" \_ 。 除了该要求之外，子单位驱动程序可以实现其控制流和资源管理机制。

    当子单位驱动程序设置 i/o 完成例程时，它可以包含 PVOID 上下文参数。 此参数可以是指向任何内容的指针，前提是已专门编写完成例程来处理它。 如果子单位驱动程序确实要使 AV/C 请求永不涉及 *过渡处理*，则 i/o 完成例程可能非常简单：使用它来触发作为 PVOID 上下文) 传递的 [**KSEVENT**](/previous-versions/ff561744(v=vs.85)) (。 用于调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 的主代码路径 (步骤5中所述的) 提供事件的存储，并使用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 与完成例程同步。 IRP 和 IRB 由主代码路径释放。

    然而，如果次级驱动程序发送的请求可能涉及过渡处理，则完成例程负责处理响应并释放 IRP 和 IRB 资源。 主代码路径让给完成例程的所有 IRP 处理责任。

5. 然后，子单位驱动程序调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，并传递下一个较低的驱动程序 (，该驱动程序将通过对 [**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) 的 **AddDevice**) 例程的调用返回，并将 IRP 处理 *Avc.sys*。

    ```cpp
    status = IoCallDriver( DeviceExtension->NextLowerDriver, Irp );
    ```

根据需要重复步骤1至5。

*Avc.sys* 尝试保证在呼叫范围内发出 AV/C 请求并且至少收到一个临时响应。 下表描述了可能的 **IoCallDriver** 返回代码，这些代码指示如何处理 AV/C 请求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_SUCCESS</p></td>
<td><p>发出了请求，并且在 AV/C 规范的超时和重试参数的界限内收到最终响应。 还必须检查子单位的响应代码 (<a href="/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb" data-raw-source="[&lt;strong&gt;AVC_COMMAND_IRB&lt;/strong&gt;](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)"><strong>AVC_COMMAND_IRB</strong></a>结构的<strong>ResponseCode</strong>成员) ，以确定操作的实际结果。 STATUS_SUCCESS 只是意味着往返请求和响应周期已在100毫秒内完成， (假定默认超时未从 100 ms) 更改。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_TIMEOUT</p></td>
<td><p>发出了请求，但在所有超时和重试处理完成之前未收到响应。 请注意，如果仍在处理以前的请求，则目标 AV/C 设备将忽略请求。 某些 AV/C 设备不符合要求，在 100 ms 超时时间内（即使几次连续尝试）也不会被拒绝。 AVC_COMMAND_IRB 结构允许 (100 ms 和 9 ms 之间分别调整默认 <strong>超时</strong> 值和 <strong>重试</strong> 成员) ，但这些默认设置已足以满足所有已知的实现要求。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_PENDING</p></td>
<td><p>发出了请求，但收到了过渡响应。 子单位驱动程序的 i/o 完成例程负责处理最后的响应，然后释放 IRP 和 IRB 资源。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p><em>Avc.sys</em> 结束了操作，可能有多种原因。</p>
<p>AV/C 命令/请求在收到过渡响应之后正在等待响应，但已将 IEEE 1394 总线重置 (并且子) 不会将这些命令悄悄地丢弃。</p>
<p>内部 AV/C IRP 处理已异常终止，因此所有未完成的命令都将停止，但命令可能仍会在) 设备上运行。</p>
<p>已拔下了次级，或已禁用 <em>Avc.sys</em> (例如，设备管理器) 。</p>
<p>在所有这些情况下，如果错误条件是暂时性的，则子单位驱动程序应重试该命令。</p></td>
</tr>
</tbody>
</table>

**IoCallDriver**中的任何其他返回值都指示发生了超出 AV/C 协议范围的错误。 例如：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_NO_SUCH_DEVICE</p></td>
<td><p>设备已拔出。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>系统内存不足。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_INVALID_PARAMETER</p></td>
<td><p>向 <em>Avc.sys</em>传递的参数无效。</p></td>
</tr>
</tbody>
</table>

基本 IRP 处理允许更低的驱动程序以同步方式完成 IRP (立即) ，或推迟其完成时间，直到晚些。 当操作延迟时，IRP 会被标记为 "挂起"，较低的驱动程序将 \_ 从该驱动程序各自的调度例程返回 "挂起" 状态，后者将返回到子单位驱动程序作为从 **IoCallDriver**返回的代码。 *Avc.sys* 将 AV/C 命令/响应协议转换为此模型。

导致立即 (同步) 响应的任何 AV/C *状态* 或 *查询* 请求在 **IoCallDriver** 调用范围内完全完成。 从 **IoCallDriver** 立即返回的指示响应发生在 Av/c 规范中详细说明的 100 ms AV/C 响应超时限制内。

仅当存在错误情况时， *通知* 请求才会立即响应。

某些 *控制* 和所有 *通知* 请求都将在100毫秒内确认请求，但可能不一定全部完成。 确认是通过一个过渡响应来完成的，这在此文档中称为 " *过渡处理*"。 过渡响应的结果是 **IoCallDriver** 返回状态 "挂起" \_ 。 如果出现此结果，则在上述步骤4中指定的 i/o 完成例程是 AV/C 子位置最终完成请求时的通知点。

有关 Irp 和 IOCTLs 的详细信息，请参阅 [处理 irp](../kernel/handling-irps.md)。
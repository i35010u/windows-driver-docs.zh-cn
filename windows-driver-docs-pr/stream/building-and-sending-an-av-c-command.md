---
title: 生成和发送 AV/C 命令
description: 生成和发送 AV/C 命令
ms.assetid: 0f5bb205-7ffe-4007-bb66-a77889af2eed
keywords:
- Avc.sys 功能驱动程序 WDK、 生成和发送命令
- 命令构建 WDK AV/C
- 命令发送 WDK AV/C
- AV/C WDK 命令
- Irp WDK AV/C
- I/O WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bb57f25be16697f8d6b65999e41c2d42cd4efad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554893"
---
# <a name="building-and-sending-an-avc-command"></a>生成和发送 AV/C 命令

以下过程概述了此过程来生成并发送 AV/C 命令：

1. 子单元驱动程序必须分配并初始化 IRP 适合自身的下方的驱动程序的数量 (下一步的较低司机的设备中指定的那样\_对象的&gt;**StackSize**成员)。 由驱动程序编写器实现的 IRP 管理的样式会影响如何获取 IRP 用于*Avc.sys*。 通常，微型驱动程序会调用[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)为 AV/C 命令分配新 IRP。 不要调用[ **IoInitializeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549315)上分配到子单元的驱动程序通过 IRP **IoAllocateIrp**。 而不是尝试以重新初始化并重复使用旧 IRP，调用[ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113)上的现有 IRP，然后调用**IoAllocateIrp**来分配新 IRP。

    > [!NOTE]
    > 为了提高可读性，下面的代码示例不演示错误处理。

    ```cpp
    PIRP Irp;
    Irp = IoAllocateIrp(DeviceExtension->ParentDeviceObject->StackSize, FALSE);
    ```

2. 子单元驱动程序然后分配 AVC\_命令\_IRB 或 AVC\_MULTIFUNC\_IRB 结构，它是适用于类型的所需的 AV/C 函数并填充具有所需的 AV/C 请求的块参数。 每个 IOCTL 的参考页\_AVC\_类函数描述函数需要哪些 IRB。 IRB 是描述 AV/C 操作码和要执行的操作的数据块。 支持的每个函数*Avc.sys*与特定 IRB 结构相关联。 必须从非分页缓冲池分配 IRB 的内存。 当已分配的内存 IRB 填写根据其关联的结构定义函数的参数。

    有关可用的函数及其关联的结构定义的列表，请参阅[AV/C 协议驱动程序函数代码](https://msdn.microsoft.com/library/windows/hardware/ff556389)， [AV/C 结构](https://msdn.microsoft.com/library/windows/hardware/ff556422)，并[AV/C 枚举](https://msdn.microsoft.com/library/windows/hardware/ff556375).

    以下是一个代码示例，演示如何 AVC\_命令\_IRB 结构可能会分配并初始化包含单个操作数字节 AV/C 控制命令：

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

3. 子单元驱动程序必须指定 IRP **MajorFunction**并**Parameters.DeviceIoControl.IoControlCode**成员，以及指向在步骤 2 中已分配 IRB 的指针。 分配 IRP 从操作系统，则为相应 IRB，分配非分页的内存，然后设置的参数，为 IRB 后，必须将 IRB 与 IRP 相关联。 具体取决于 IRB 的函数代码中，必须以 IRP 指定正确的调度例程。 AV/C 函数代码对应于 IOCTL\_AVC\_类 (即**Parameters.DeviceIoControl.IoControlCode**成员设置为 IOCTL\_AVC\_类)，IRP\_MN\_内部\_设备\_控件必须指定为已分配 IRP **MajorFunction**值。 支持的所有其他 AV/C 函数代码*Avc.sys*，如[ **IOCTL\_AVC\_更新\_虚拟\_子单元\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560798)， [ **IOCTL\_AVC\_删除\_虚拟\_子单元\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff560793)，和[**IOCTL\_AVC\_总线\_重置**](https://msdn.microsoft.com/library/windows/hardware/ff560783)，必须指定 IRP\_MJ\_设备\_控件作为分配 IRP 的**MajorFunction**值。

    下面的代码示例演示如何设置 IRP *Avc.sys*到进程：

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

4. 子单元驱动程序必须为 IRP，最小值，用以分析响应中指定的 I/O 完成例程。 完成例程还可以释放以前分配的同步未完成的 Irp 的 IRP 和 IRB 资源 （即，完成例程仅释放的 IRP 和 IRB 资源如果 IRP 被标记为挂起之前）。

    需要的 I/O 完成例程，因为子单元驱动程序必须分配与进行通信的 Irp *Avc.sys*。 完成例程会继续处理子单元驱动程序的已分配的 IRP 到较低的驱动程序的子单元的调用完成后阻止 I/O 管理器。 I/O 完成例程必须始终返回状态\_更多\_处理\_必需。 超出这一要求，子单元驱动程序可能会实现其控制流和资源管理机制。

    当子单元驱动程序设置 I/O 完成例程时，它可以包括 PVOID 上下文参数。 此参数可以是指向任何内容，只要完成例程专门编写是为了解决这个问题。 如果子单元的驱动程序确保 AV/C 请求永远不会涉及*临时处理*，则 I/O 完成例程可以是非常简单： 使用它来触发[ **KSEVENT** ](https://msdn.microsoft.com/library/windows/hardware/ff561744)（作为 PVOID 上下文传递）。 调用的主代码路径[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) （在步骤 5 中所述） 的事件，提供存储，并使用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)与完成例程进行同步。 IRP 和 IRB 会释放由主代码路径。

    如果，但是，子单元驱动程序发送的请求，可能会涉及到临时处理，完成例程负责处理响应和释放的 IRP 和 IRB 资源。 主代码路径放弃所有 IRP 处理职责交给完成例程。

5. 然后调用子单元驱动程序[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) ，并将传递的下一个较低的驱动程序 (通过调用返回[ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300)中的子单元驱动程序**AddDevice**例程) 和 IRP 到处理*Avc.sys*。

    ```cpp
    status = IoCallDriver( DeviceExtension->NextLowerDriver, Irp );
    ```

重复步骤 1 至 5 根据需要。

*Avc.sys*尝试保证 AV/C 请求和调用的范围内收到至少是临时的响应。 下表描述了可能**IoCallDriver**返回代码，以表明如何处理 AV/C 请求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_SUCCESS</p></td>
<td><p>发出请求，并最终响应收到 AV/C 规范的边界内&#39;s 超时和重试参数。 子单元&#39;s 响应代码 ( <strong>ResponseCode</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff554140" data-raw-source="[&lt;strong&gt;AVC_COMMAND_IRB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554140)"> <strong>AVC_COMMAND_IRB</strong> </a>结构) 仍必须检查来确定的则返回 true 的结果操作。 STATUS_SUCCESS 指的是双向的请求和响应周期已完成中小于 100 毫秒 （假定默认超时值已改变的 100 毫秒）。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_TIMEOUT</p></td>
<td><p>发出请求，但未收到响应之前所有的超时和重试处理已完成。 请注意，是否上一个请求仍在处理目标 AV/C 设备请求将忽略。 某些 AV/C 的设备不符合并拒绝内 100 毫秒的超时值，即使在多次连续尝试后响应。 AVC_COMMAND_IRB 结构允许的默认值调整<strong>超时</strong>并<strong>重试</strong>成员 (100 ms 和 9 毫秒，分别)，但这些默认设置已经足够所有已知实现。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_PENDING</p></td>
<td><p>发出请求，并收到了临时的响应。 它负责子单元驱动程序的&#39;s I/O 完成例程来处理最终响应，然后释放的 IRP 和 IRB 资源。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p><em>Avc.sys</em>已结束操作，这种情况的原因。</p>
<p>AV/C 命令/请求已等待的响应后未收到了临时的响应，但 IEEE 1394 总线已重置 （和子单元将以无提示方式删除这些命令）。</p>
<p>内部 AV/C IRP 已异常终止处理，因此任何未完成的命令已停止，但命令仍可能在设备上进行)。</p>
<p>子单元被拔出，或<em>Avc.sys</em>已被禁用 （例如从设备管理器）。</p>
<p>在所有这些情况下，子单元驱动程序应重试该命令，以防是暂时性的错误条件。</p></td>
</tr>
</tbody>
</table>

从任何其他返回值**IoCallDriver**指示发生了错误，已超出范围的 AV/C 协议。 例如：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>描述</th>
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
<td><p>无效的参数传递给<em>Avc.sys</em>。</p></td>
</tr>
</tbody>
</table>

基本的 IRP 处理允许较低的驱动程序无法以同步方式完成 IRP （立即），或延迟更高版本直到其完成。 如果延迟操作，IRP 被标记为挂起，并且较低的驱动程序将返回状态\_从该驱动程序的各自的调度例程，它是返回子单元驱动程序的返回代码为 PENDING **IoCallDriver**. *Avc.sys*转换到此模型的 AV/C 命令/响应协议。

任何 AV/C*状态*或*查询*导致即时 （同步） 响应的请求已完全完成的跨度**IoCallDriver**调用。 立即返回从**IoCallDriver**指示响应时间内 AV/C 规格中详述的 100 ms AV/C 响应超时约束。

一个*通知*请求响应立即仅当没有错误条件。

某些*控制*和全部*通知*请求确认，但可能不一定完成，在 100 毫秒内的请求。 确认是通过在本文档中引用的临时响应*临时处理*。 临时响应的结果是， **IoCallDriver**将返回状态\_PENDING。 如果出现这种结果，则在第 4 步中指定的 I/O 完成例程的通知点 AV/C 子单元由最后完成请求时。

有关 Irp 和 Ioctl 的详细信息，请参阅[处理 Irp](https://msdn.microsoft.com/library/windows/hardware/ff546847)。

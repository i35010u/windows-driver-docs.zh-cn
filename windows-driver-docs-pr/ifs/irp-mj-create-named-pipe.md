---
title: IRP_MJ_CREATE_NAMED_PIPE
description: IRP_MJ_CREATE_NAMED_PIPE
ms.assetid: 0efa732c-b6e8-4ddf-a897-389153b69ab3
keywords:
- IRP_MJ_CREATE_NAMED_PIPE 文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_CREATE_NAMED_PIPE
api_type:
- NA
ms.date: 11/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: a80608b03dc673f4cf288de343ff4196e67f9957
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065556"
---
# <a name="irp_mj_create_named_pipe"></a>IRP_MJ_CREATE_NAMED_PIPE

## <a name="when-sent"></a>发送时间

当创建或打开新的命名管道时，i/o 管理器将发送 IRP_MJ_CREATE_NAMED_PIPE 请求。 通常，发送此 IRP：

- 代表已调用 Microsoft Win32 函数（如 [**CreateNamedPipe**](/windows/win32/api/winbase/nf-winbase-createnamedpipea)）的用户模式应用程序。
- 或者代表已调用 [**IoCreateFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile) 或 [**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的内核模式组件。

如果命名管道创建请求成功完成，则应用程序或内核模式组件会接收命名管道文件实例的服务器端的句柄。

IRP_MJ_CREATE_NAMED_PIPE 的处理与 [IRP_MJ_CREATE](irp-mj-create.md)几乎相同。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序

如果目标设备对象是文件系统的控制设备对象，则在将 *irp >IoStatus* 和 *IRP >IoStatus* 设置为合适的值后，文件系统驱动程序的调度例程必须完成 irp 并返回相应的 NTSTATUS 值。

否则，文件系统驱动程序应处理创建请求。

## <a name="operation-file-system-legacy-filter-drivers"></a>操作：文件系统旧筛选器驱动程序

如果目标设备对象是旧筛选器驱动程序的控制设备对象，则在设置 *irp >IoStatus* 和 *IRP->IoStatus* 为适当值后，该驱动程序的调度例程必须完成 irp 并返回相应的 NTSTATUS 值。

否则，旧筛选器驱动程序应执行任何所需的处理，并根据筛选器的性质，完成 IRP，或将其向下传递到堆栈上的下一个较低版本的驱动程序。

通常，旧筛选器驱动程序不应返回 **STATUS_PENDING** 来响应 IRP_MJ_CREATE_NAMED_PIPE。 但是，如果较低级别的驱动程序返回 **STATUS_PENDING**，则旧筛选器驱动程序应将此状态值向上传递到驱动程序链。

## <a name="parameters"></a>parameters

文件系统或旧筛选器驱动程序使用给定的 IRP 调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 irp 中的 [**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location) 的指针。 在下面的参数中， *irp* 指向 irp，并 *IrpSp* 指向 IO_STACK_LOCATION。 驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理创建请求。

- *DeviceObject* 是指向目标设备对象的指针。

- *Irp-* 对于此请求，>标志设置为以下标志：
  - IRP_CREATE_OPERATION
  - IRP_DEFER_IO_COMPLETION
  - IRP_SYNCHRONOUS_API

- *Irp->IoStatus* 指向 [IO_STATUS_BLOCK](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构，该结构接收最终完成状态和有关请求的操作的信息。 文件系统将此结构的 **信息** 成员设置为以下值之一：
  - FILE_CREATED
  - FILE_OPENED

- *Irp->irp->requestormode* 指示请求操作的进程的执行模式，可以是 **KernelMode** 或 **UserMode**。 请注意，如果设置了 SL_FORCE_ACCESS_CHECK 标志，则即使 *Irp >irp->requestormode* 为 **KernelMode**，也必须执行访问检查。

- *IrpSp->MajorFunction* 设置为 IRP_MJ_CREATE_NAMED_PIPE。
  
  - *IrpSp->标志* 可设置为 SL_FORCE_ACCESS_CHECK。 如果设置此标志，则即使 *Irp >irp->requestormode* 的值为 **KernelMode**，也必须执行访问检查。

- *IrpSp->CreatePipe。 SecurityContext->AccessState* 是一个指向 [ACCESS_STATE](/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state) 结构的指针，该结构包含对象的主题上下文、授予访问类型和剩余所需的访问类型。

- *IrpSp->CreatePipe. SecurityContext->DesiredAccess* 是一个 ACCESS_MASK 结构，该结构指定为命名管道请求的访问权限。 有关详细信息，请参阅[**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的*DesiredAccess*参数说明。

- *IrpSp->参数. CreatePipe* 是标志的位掩码，用于指定创建或打开命名管道时要应用的选项，以及命名管道已经存在时要执行的操作。

  此参数的高8位对应于[**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的*处置*参数。

  此成员的低24位对应于[**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的*CreateOptions*参数。

- *IrpSp->参数. CreatePipe. ShareAccess* 是命名管道请求的共享访问权限位掩码。 如果此成员为零，则请求进行独占访问。 有关详细信息，请参阅[**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的*ShareAccess*参数说明。

- *IrpSp->参数. CreatePipe. 参数* 是指向 [NAMED_PIPE_CREATE_PARAMETERS](/windows-hardware/drivers/ddi/wdm/ns-wdm-_named_pipe_create_parameters) 结构的指针，该结构包含创建命名管道时的 CREATE 参数。

- *IrpSp->FileObject* 一个指针，指向 i/o 管理器创建的文件对象，该对象表示要创建或打开的命名管道。 当文件系统处理 IRP_MJ_CREATE_NAMED_PIPE 请求时，它会将此文件对象中的 **FsContext** 和可能的 **FsContext2** 字段设置为特定于文件系统的值。 因此，在文件系统处理创建请求之前，不能将 **FsContext** 和 **FsContext2** 字段的值视为有效。 有关详细信息，请参阅 [文件流、流上下文和每个流的上下文](./file-streams--stream-contexts--and-per-stream-contexts.md)。

  [**IoCancelFileOpen**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen) (和 [**FltCancelFileOpen**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)) 在文件对象的 " **标志** " 字段中设置 FO_FILE_OPEN_CANCELLED 标志。 设置此标志指示 IRP_MJ_CREATE_NAMED_PIPE 请求已取消，并将为此文件对象发出 [**IRP_MJ_CLOSE**](irp-mj-close.md) 请求。 一旦取消创建请求，就无法重新颁发。

  *>IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是 FILE_OBJECT 的结构。 FILE_OBJECT 结构的 " **RelatedFileObject** " 字段用于指示已相对于已打开的文件对象打开给定的命名管道。 这通常表示相对文件是一个目录，但基于流的文件可能会相对于现有的文件流打开。 FILE_OBJECT 结构的 **RelatedFileObject** 字段仅在处理 IRP_MJ_CREATE_NAMED_PIPE 期间有效。

## <a name="see-also"></a>请参阅

[ACCESS_MASK](../kernel/access-mask.md)

[ACCESS_STATE](/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[FLT_PARAMETERS](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[IRP_MJ_CREATE_NAMED_PIPE 的 FLT_PARAMETERS](flt-parameters-for-irp-mj-create-named-pipe.md)

[**FltCancelFileOpen**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)

[IO_STACK_LOCATION](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[IO_STATUS_BLOCK](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCancelFileOpen**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen)

[**IoCreateFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)

[**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)

[**IoCreateStreamFileObject**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[IRP](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[IRP_MJ_CLEANUP](irp-mj-cleanup.md)

[IRP_MJ_CLOSE](irp-mj-close.md)

[ (WDK 内核引用 IRP_MJ_CREATE) ](../kernel/irp-mj-create.md)

[NAMED_PIPE_CREATE_PARAMETERS](/windows-hardware/drivers/ddi/wdm/ns-wdm-_named_pipe_create_parameters)
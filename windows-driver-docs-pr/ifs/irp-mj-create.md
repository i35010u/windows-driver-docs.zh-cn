---
title: 'IRP_MJ_CREATE (IFS) '
description: IRP_MJ_CREATE
keywords:
- IRP_MJ_CREATE 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_CREATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b810c67abd05774fe6052ec1d27a7a6c272bf14a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840731"
---
# <a name="irp_mj_create-ifs"></a>IRP_MJ_CREATE (IFS) 

## <a name="when-sent"></a>发送时间

创建新文件或目录时，或在打开现有文件、设备、目录或卷时，i/o 管理器将发送 IRP_MJ_CREATE 请求。

通常，此 IRP 是代表用户模式应用程序发送的，该应用程序已调用 Microsoft Win32 函数（如 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) ）或代表已调用函数（如 [**IoCreateFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)、 [**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)、 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)或 [**ZwOpenFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)）的内核模式组件。

如果创建请求成功完成，则应用程序或内核模式组件会接收文件对象的句柄。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序

如果目标设备对象是文件系统的控制设备对象，则在将 *irp >IoStatus* 和 *IRP >IoStatus* 设置为合适的值后，文件系统驱动程序的调度例程必须完成 irp 并返回相应的 NTSTATUS 值。

否则，文件系统驱动程序应处理创建请求。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序

如果目标设备对象是筛选器驱动程序的控制设备对象，则筛选器驱动程序的调度例程必须完成 IRP 并返回相应的 NTSTATUS 值，然后将 IoStatus 设置为相应的值，然后再 *>* 将 Irp *>IoStatus。*

否则，筛选器驱动程序应执行任何所需的处理，并根据筛选器的性质，完成 IRP，或将其向下传递到堆栈上的下一个较低的驱动程序。

通常，筛选器驱动程序不应返回 **STATUS_PENDING** 来响应 **IRP_MJ_CREATE**。 但是，如果较低级别的驱动程序返回 **STATUS_PENDING**，则筛选器驱动程序应将此状态值向上传递到驱动程序链。

文件系统筛选器驱动程序编写器应注意到， [**IoCreateStreamFileObject**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject) 导致 [**IRP_MJ_CLEANUP**](irp-mj-cleanup.md) 请求发送到卷的文件系统驱动程序堆栈。 由于文件系统通常会将流文件对象创建为 **IRP_MJ_CREATE** 以外的操作的副作用，因此筛选器驱动程序很难可靠地检测流文件对象创建。 因此，筛选器驱动程序应该接收到 **IRP_MJ_CLEANUP** 和 [**IRP_MJ_CLOSE**](../kernel/irp-mj-close.md) 对以前不可见的文件对象的请求。 对于 [**IoCreateStreamFileObjectLite**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)，不会发送 **IRP_MJ_CLEANUP** 请求。

> [!NOTE]
> 当旧筛选器驱动程序在创建后回调中重新发出 create 时，它们必须释放并设置与其重新分析点相关联的缓冲区 (辅助缓冲区) 为 **NULL**。 如果旧筛选器驱动程序未释放此缓冲区并将其设置为 **NULL**，则驱动程序将泄漏内存。 微筛选器驱动程序不一定要这样做，因为筛选器管理器会为其执行此操作。

## <a name="parameters"></a>参数

文件系统或筛选器驱动程序与给定的 IRP 一起调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 *IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在进程创建请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

* *DeviceObject*：指向目标设备对象的指针。

* *Irp->AssociatedIrp.SystemBuffer*：指向 [**FILE_FULL_EA_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构缓冲区的指针，如果该文件对象表示具有扩展属性的文件。 否则，此成员设置为 **NULL**。

* *Irp >标志*：为此请求设置以下标志：

  * IRP_CREATE_OPERATION
  * IRP_DEFER_IO_COMPLETION
  * IRP_SYNCHRONOUS_API

* *Irp->irp->requestormode*：指示请求操作的进程的执行模式，为 **KernelMode** 或 **UserMode**。 请注意，如果设置了 SL_FORCE_ACCESS_CHECK 标志，则即使 *Irp >irp->requestormode* 为 **KernelMode**，也必须执行访问检查。

* *Irp->IoStatus*：指向 [**IO_STATUS_BLOCK**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。 文件系统将此结构的 **信息** 成员设置为以下值之一：

  * FILE_CREATED
  * FILE_DOES_NOT_EXIST
  * FILE_EXISTS
  * FILE_OPENED
  * FILE_OVERWRITTEN
  * FILE_SUPERSEDED

* *Irp->AllocationSize*：文件的初始分配大小（以字节为单位）。 如果创建、覆盖或取代了文件，则非零值将不起作用。

* *IrpSp->FileObject*：指向 I/o 管理器创建以表示要创建或打开的文件的文件对象的指针。 当文件系统处理 IRP_MJ_CREATE 请求时，它会将此文件对象中的 **FsContext** 和可能的 **FsContext2** 字段设置为特定于文件系统的值。 因此，在文件系统处理创建请求之前，不能将 **FsContext** 和 **FsContext2** 字段的值视为有效。 有关详细信息，请参阅 [文件流、流上下文和 Per-Stream 上下文](file-streams--stream-contexts--and-per-stream-contexts.md)。

  [**FltCancelFileOpen**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen) 和 [**IoCancelFileOpen**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen) 在文件对象的 " **标志** " 字段中设置 FO_FILE_OPEN_CANCELLED 标志。 设置此标志指示 IRP_MJ_CREATE 请求已取消，并将为此文件对象发出 [**IRP_MJ_CLOSE**](irp-mj-close.md) 请求。 一旦取消创建请求，就无法重新颁发。

  *>IrpSp FileObject* 参数包含指向 **RelatedFileObject** 字段的指针，该字段也是 FILE_OBJECT 的结构。 FILE_OBJECT 结构的 " **RelatedFileObject** " 字段用于指示给定文件是相对于已打开的文件对象打开的。 这通常表示相对文件是一个目录，但基于流的文件可能会相对于现有的文件流打开。 FILE_OBJECT 结构的 **RelatedFileObject** 字段仅在处理 IRP_MJ_CREATE 期间有效。

* *IrpSp->标志*：以下一个或多个值：

  | 标志 | 含义 |
  | ---- | ------- |
  | SL_FORCE_ACCESS_CHECK 0x01 | 如果设置此标志，则即使 *IRP >irp->requestormode* 的值为 **KernelMode**，也必须执行访问检查。 |
  | SL_OPEN_PAGING_FILE 0x02 | 如果设置了此标志，则该文件为页面文件。 |
  | SL_OPEN_TARGET_DIRECTORY 0x04 | 如果设置此标志，则应打开文件的父目录。 |
  | SL_STOP_ON_SYMLINK 0x08 | 如果设置了此标志，则会取消 i/o 管理器的联接和符号链接的自动遍历，导致打开联接和符号链接以返回 STATUS_REPARSE。 |
  | SL_IGNORE_READONLY_ATTRIBUTE 0x40 | 如果设置了此标志，则它允许创建一个只读文件和 FILE_DELETE_ON_CLOSE 选项，这将导致在关闭该句柄时删除文件。 |
  | SL_CASE_SENSITIVE 0x80 | 如果已设置，则文件名比较应区分大小写。 |
  
* *IrpSp->MajorFunction*：指定 IRP_MJ_CREATE。

* *IrpSp->EaLength：* 的 *AssociatedIrp.Sys>* 缓冲区大小（以字节为单位）。 如果 *Irp >AssociatedIrp.SystemBuffer* 的值为 **NULL**，则此成员必须为零。

* *IrpSp->FileAttributes*：创建或打开文件时要应用的特性标志的位掩码。 仅当创建、取代或在某些情况下覆盖了文件时，才应用显式指定的属性。 默认情况下，此值为 FILE_ATTRIBUTE_NORMAL，这可以由任何其他标志或兼容标志的运算组合重写。 此成员对应于 [**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的 *FileAttributes* 参数。

* *IrpSp->参数。创建。选项*：标志的位掩码，用于指定创建或打开文件时要应用的选项，以及在文件已存在时要执行的操作。

  此参数的高8位对应于 [**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的 *处置* 参数。

  此成员的低24位对应于 [**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的 *CreateOptions* 参数。 执行文件扫描 (文件系统筛选器和微筛选器驱动程序（如防病毒程序) 应特别注意 FILE_COMPLETE_IF_OPLOCKED 标志。 如果设置了此标志，则筛选器不能阻止或延迟 IRP_MJ_CREATE 操作。

  如果在预创建 (创建调度) 路径中设置了 FILE_COMPLETE_IF_OPLOCKED 标志，则筛选器不能启动以下任何类型的操作，因为它们可能会导致 oplock 中断：

  * IRP_MJ_CLEANUP
  * IRP_MJ_CREATE
  * IRP_MJ_FILE_SYSTEM_CONTROL
  * IRP_MJ_FLUSH_BUFFERS
  * IRP_MJ_LOCK_CONTROL
  * IRP_MJ_READ
  * IRP_MJ_SET_INFORMATION
  * IRP_MJ_WRITE

  如果筛选器或微筛选器不能服从 FILE_COMPLETE_IF_OPLOCKED 标志，则必须使用 STATUS_SHARING_VIOLATION 完成 IRP_MJ_CREATE 请求。

  如果在完成 (创建后) 路径中设置了 FILE_COMPLETE_IF_OPLOCKED 标志，则筛选器应检查文件系统是否已将 *Irp->IoStatus* 设置为 STATUS_OPLOCK_BREAK_IN_PROGRESS 状态值。 如果未设置此状态值，筛选器将对该文件启动上述一项操作是安全的。 如果设置此状态值，则 oplock 尚未中断，筛选器不能启动可能导致 oplock 中断的任何操作。 因此，在满足以下条件之一之前，筛选器必须将上述所有操作推迟到该文件中：

  * Oplock 的所有者将 FSCTL_OPLOCK_BREAK_ACKNOWLEDGE 请求发送到文件系统。
  * 除筛选器或微筛选器外的系统组件会向文件系统发送必须等待 oplock 中断完成的 i/o 请求， (如 IRP_MJ_READ 或 IRP_MJ_WRITE) 。 筛选器或微筛选器可以从其调度 (或 preoperation 回调) 例程为此新操作启动上述操作之一，因为调度或 preoperation 回调例程将进入等待状态，直到 oplock 中断完成。

* *IrpSp->SecurityContext->AccessState*：指向一个 [**ACCESS_STATE**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state) 结构的指针，该结构包含对象的主题上下文、授予访问类型和剩余所需的访问类型。

* *IrpSp->SecurityContext->DesiredAccess*： ACCESS_MASK 结构，指定为文件请求的访问权限。 有关详细信息，请参阅 [**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的 *DesiredAccess* 参数说明。

* *IrpSp->ShareAccess*：请求为文件提供共享访问权限的位掩码。 如果此成员为零，则请求进行独占访问。 有关详细信息，请参阅 [**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的 *ShareAccess* 参数说明。

## <a name="see-also"></a>请参阅

[**ACCESS_MASK**](../kernel/access-mask.md)

[**ACCESS_STATE**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[**FILE_FULL_EA_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**FltCancelFileOpen**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)

[**FltReissueSynchronousIo**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreissuesynchronousio)

[**IO_STACK_LOCATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO_STATUS_BLOCK**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCancelFileOpen**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen)

[**IoCheckEaBufferValidity**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoCreateFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)

[**IoCreateFileSpecifyDeviceObjectHint**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)

[**IoCreateStreamFileObject**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP_MJ_CLEANUP**](irp-mj-cleanup.md)

[**IRP_MJ_CLOSE**](irp-mj-close.md)

[**(WDK 内核引用 IRP_MJ_CREATE)**](../kernel/irp-mj-create.md)

[**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

[**ZwOpenFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)

---
title: IRP_MJ_CREATE_MAILSLOT
description: IRP_MJ_CREATE_MAILSLOT
ms.assetid: 6cd04fd0-ee36-421f-8877-f409aba31b17
keywords:
- IRP_MJ_CREATE_MAILSLOT 文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_CREATE_MAILSLOT
api_type:
- NA
ms.date: 11/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: 44a0c83a7e6e95f30db7eb99aac75999bdbd995c
ms.sourcegitcommit: 257850d61aa5d1db707dc2f30721319b650e47f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2019
ms.locfileid: "73801163"
---
# <a name="irp_mj_create_mailslot"></a>IRP_MJ_CREATE_MAILSLOT

## <a name="when-sent"></a>发送时间

创建或打开新的 MAILSLOT 时，i/o 管理器将发送 IRP_MJ_CREATE_MAILSLOT 请求。 通常，发送此 IRP：

- 代表已调用 Microsoft Win32 函数（如[**CreateMailslot**](https://docs.microsoft.com/windows/win32/api/winbase/nf-winbase-createmailslota)）的用户模式应用程序。
- 或者代表已调用[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)或[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的内核模式组件。

如果 mailslot create 请求成功完成，则应用程序或内核模式组件会接收 mailslot 文件实例的句柄。

IRP_MJ_CREATE_MAILSLOT 的处理与[IRP_MJ_CREATE](irp-mj-create.md)几乎相同。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序

如果目标设备对象是文件系统的控制设备对象，则在设置*irp > IoStatus*和 IRP 后，文件系统驱动程序的调度例程必须完成 irp 并返回相应的 NTSTATUS 值 *>IoStatus*为适当的值。

否则，文件系统驱动程序应处理创建请求。

## <a name="operation-file-system-legacy-filter-drivers"></a>操作：文件系统旧筛选器驱动程序

如果目标设备对象是旧筛选器驱动程序的控制设备对象，则在设置*irp > IoStatus*和 IRP 后，该驱动程序的调度例程必须完成 irp 并返回相应的 NTSTATUS 值 *>IoStatus*为适当的值。

否则，旧筛选器驱动程序应执行任何所需的处理，并根据筛选器的性质，完成 IRP，或将其向下传递到堆栈上的下一个较低版本的驱动程序。

通常，旧筛选器驱动程序不应返回**STATUS_PENDING**来响应**IRP_MJ_CREATE_MAILSLOT**。 但是，如果较低级别的驱动程序返回**STATUS_PENDING**，则旧筛选器驱动程序应将此状态值向上传递到驱动程序链。

## <a name="parameters"></a>参数

文件系统或旧筛选器驱动程序使用给定的 IRP 调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 irp 中的[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针。 在下面的参数中， *irp*指向 irp，并*IrpSp*指向 IO_STACK_LOCATION。 驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理创建请求：

- *DeviceObject*是指向目标设备对象的指针。

- *Irp-* 对于此请求，> 标志设置为以下标志：
  - IRP_CREATE_OPERATION
  - IRP_DEFER_IO_COMPLETION
  - IRP_SYNCHRONOUS_API

- *Irp-> IoStatus*指向[IO_STATUS_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，该结构接收最终完成状态和有关请求的操作的信息。 文件系统将此结构的**信息**成员设置为以下值之一：
  - FILE_CREATED
  - FILE_OPENED

- *Irp-> irp->requestormode*指示请求操作的进程的执行模式，可以是**KernelMode**或**UserMode**。 请注意，如果设置了 SL_FORCE_ACCESS_CHECK 标志，则即使*Irp > irp->requestormode*为**KernelMode**，也必须执行访问检查。

- *IrpSp-> MajorFunction*设置为 IRP_MJ_CREATE_MAILSLOT。

- *IrpSp-> 标志*可设置为 SL_FORCE_ACCESS_CHECK。 如果设置此标志，则即使*Irp > irp->requestormode*的值为**KernelMode**，也必须执行访问检查。

- *IrpSp-> CreateMailslot。 SecurityContext-> AccessState*是一个指向[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)结构的指针，该结构包含对象的主题上下文、授予访问类型和剩余所需的访问类型。

- *IrpSp-> CreateMailslot. SecurityContext-> DesiredAccess*是一个 ACCESS_MASK 结构，该结构指定为 mailslot 请求的访问权限。 有关详细信息，请参阅[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的*DesiredAccess*参数说明。

- *IrpSp-> 参数. CreateMailslot*是标志的位掩码，用于指定创建或打开 mailslot 时要应用的选项，以及当 mailslot 已经存在时要执行的操作。

  此参数的高8位对应于[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的*处置*参数。

  此成员的低24位对应于[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的*CreateOptions*参数。

- *IrpSp-> 参数. CreateMailslot. ShareAccess*是为 mailslot 请求的共享访问权限位掩码。 如果此成员为零，则请求进行独占访问。 有关详细信息，请参阅[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)的*ShareAccess*参数说明。

- *IrpSp-> 参数. CreateMailslot. 参数*是指向[MAILSLOT_CREATE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mailslot_create_parameters)结构的指针，该结构包含创建 MAILSLOT 时的 CREATE 参数。

- *IrpSp-> FileObject*是一个指针，指向 I/o 管理器创建的文件对象，用于表示要创建或打开的 mailslot。 当文件系统处理 IRP_MJ_CREATE_MAILSLOT 请求时，它会将此文件对象中的**FsContext**和可能的**FsContext2**字段设置为特定于文件系统的值。 因此，在文件系统处理创建请求之前，不能将**FsContext**和**FsContext2**字段的值视为有效。 有关详细信息，请参阅[文件流、流上下文和每个流的上下文](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-streams--stream-contexts--and-per-stream-contexts)。

  [**IoCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen) （和[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)）设置文件对象的 "**标志**" 字段中的 FO_FILE_OPEN_CANCELLED 标志。 设置此标志指示 IRP_MJ_CREATE_MAILSLOT 请求已取消，并将为此文件对象发出[**IRP_MJ_CLOSE**](irp-mj-close.md)请求。 一旦取消创建请求，就无法重新颁发。

  *> IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是 FILE_OBJECT 的结构。 FILE_OBJECT 结构的 " **RelatedFileObject** " 字段用于指示给定的 mailslot 是相对于已打开的文件对象打开的。 这通常表示相对文件是一个目录，但基于流的文件可能会相对于现有的文件流打开。 FILE_OBJECT 结构的**RelatedFileObject**字段仅在处理 IRP_MJ_CREATE_MAILSLOT 期间有效。

## <a name="see-also"></a>另请参阅

[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[IRP_MJ_CREATE_MAILSLOT 的 FLT_PARAMETERS](flt-parameters-for-irp-mj-create-mailslot.md)

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)

[IO_STACK_LOCATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[IO_STATUS_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen)

[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)

[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[IRP](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[IRP_MJ_CLEANUP](irp-mj-cleanup.md)

[IRP_MJ_CLOSE](irp-mj-close.md)

[IRP_MJ_CREATE （WDK 内核参考）](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)

[MAILSLOT_CREATE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mailslot_create_parameters)

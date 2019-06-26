---
title: IRP_MJ_CREATE
description: IRP\_MJ\_CREATE
ms.assetid: fdcc81f0-e571-4194-88cd-d0956ca1577e
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
ms.openlocfilehash: d4831e1e42e874eb3741b25bc42a956fa9ca1b46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376089"
---
# <a name="irpmjcreate"></a>IRP\_MJ\_CREATE


## <a name="when-sent"></a>发送时间


I/O 管理器发送 IRP\_MJ\_创建请求时在创建新的文件或目录，或当现有文件，正在打开设备、 目录或卷。 通常代表一个用户模式应用程序，如调用 Microsoft Win32 函数发送此 IRP [ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)或已调用的内核模式组件代表[ **IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)， [ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)， [ **ZwCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)，或[ **ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile)。 如果成功完成创建请求，应用程序或内核模式组件接收文件对象的句柄。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果目标设备对象是文件系统控制设备对象，必须完成 IRP 和设置后返回适当的 NTSTATUS 值，文件系统驱动程序的调度例程*Irp-&gt;IoStatus.Status*并*Irp-&gt;IoStatus.Information*为适当的值。

否则，文件系统驱动程序应处理创建请求。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


如果目标设备对象是筛选器驱动程序的控制设备对象，必须完成 IRP 和返回适当的 NTSTATUS 值之后设置, 筛选器驱动程序的调度例程*Irp-&gt;IoStatus.Status*和*Irp-&gt;IoStatus.Information*为适当的值。

否则为筛选器驱动程序应执行任何所需的处理和，具体取决于筛选器的特性，完成 IRP 或在堆栈上传递给下一个较低驱动程序。

通常情况下，筛选器驱动程序不应返回**状态\_PENDING**响应**IRP\_MJ\_创建**。 但是，如果较低级驱动程序将返回**状态\_PENDING**，筛选器驱动程序应将驱动程序链此状态值传递。

文件系统筛选器驱动程序编写人员应注意[ **IoCreateStreamFileObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject)导致[ **IRP\_MJ\_清理**](irp-mj-cleanup.md)请求发送到文件系统驱动程序堆栈，供该卷。 因为文件系统通常创建流文件对象的操作的副作用以外**IRP\_MJ\_创建**，很难可靠地检测到流文件对象创建的筛选器驱动程序。 因此筛选器驱动程序应该会收到**IRP\_MJ\_清理**并[ **IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)之前未的文件对象的请求。 情况下[ **IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobjectlite)，则**IRP\_MJ\_清理**不发送请求。

&gt; \[!请注意\]&gt;旧筛选器驱动程序重新发布在创建后创建回叫，它们必须发布，并将其重新分析点 （辅助缓冲区） 关联到的缓冲区**NULL**。 如果旧的筛选器驱动程序不会不释放此缓冲区并将其设置为**NULL**，驱动程序会发生内存泄漏。 微筛选器驱动程序不需要这样做是因为筛选器管理器执行此它们。

 

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理创建请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
指向[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)的结构化的缓冲区，如果该文件对象表示具有扩展属性的文件。 否则，此成员设置为**NULL**。

<a href="" id="irp--flags"></a>*Irp-&gt;标志*  
此请求设置以下标志：

IRP\_创建\_操作

IRP\_DEFER\_IO\_完成

IRP\_同步\_API

<a href="" id="irp--requestormode"></a>*Irp-&gt;RequestorMode*指示或者请求操作的进程的执行模式**KernelMode**或**UserMode**。 请注意，如果 SL\_FORCE\_访问权限\_检查标志设置，则必须执行访问检查，即使*Irp-&gt;RequestorMode*是 KernelMode。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*指针，指向[ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)有关接收最终的完成状态和信息的结构请求的操作。 文件系统集**信息**为以下值之一的此结构的成员：

文件\_已创建

文件\_DOES\_不\_存在

文件\_EXISTS

文件\_OPENED

文件\_OVERWRITTEN

文件\_被取代

<a href="" id="irp--overlay-allocationsize"></a>*Irp-&gt;Overlay.AllocationSize*初始分配大小，以字节为单位的文件。 一个非零值无任何效果，除非创建文件时，覆盖，还是所取代。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;的文件对象*I/O 管理器创建来表示要创建或打开的文件的文件对象的指针。 文件系统时处理 IRP\_MJ\_创建请求时，它会设置**FsContext**甚至**FsContext2**值到此文件对象中的字段文件系统特定。 这样的值**FsContext**并**FsContext2**字段不会考虑有效期截止日期后的文件系统已处理创建请求。 有关详细信息，请参阅[文件流、 Stream 上下文和每个 Stream 上下文](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-streams--stream-contexts--and-per-stream-contexts)。

[**FltCancelFileOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen)并[ **IoCancelFileOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocancelfileopen)设置为\_文件\_打开\_文件对象中的已取消标志**标志**字段。 设置此标志指示 IRP\_MJ\_已取消创建请求，和一个[ **IRP\_MJ\_关闭**](irp-mj-close.md)将用于发出请求此文件对象。 一旦已取消创建请求，它不能重新发布。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**文件的字段\_对象结构用于指示给定的文件，已打开相对于已打开的文件对象。 这通常表示相对文件是一个目录，但可能会相对于文件的现有流打开基于流的文件。 **RelatedFileObject**字段的文件\_对象结构 IRP 在处理过程才有效\_MJ\_创建。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;标志*一个或多个以下：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_CASE_SENSITIVE</p></td>
<td align="left"><p>如果设置此标志，文件的名称比较应区分大小写。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_FORCE_ACCESS_CHECK</p></td>
<td align="left"><p>如果设置此标志，必须执行访问检查即使的值<em>IRP-&gt;RequestorMode</em>是<strong>KernelMode</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_OPEN_PAGING_FILE</p></td>
<td align="left"><p>如果设置此标志，该文件是分页文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_OPEN_TARGET_DIRECTORY</p></td>
<td align="left"><p>如果设置此标志，则应打开文件的父目录。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction* IRP 指定\_MJ\_创建。

<a href="" id="irpsp--parameters-create-ealength"></a>*IrpSp-&gt;Parameters.Create.EaLength*以字节为单位的缓冲区的大小*Irp-&gt;AssociatedIrp.SystemBuffer*。 如果的值*Irp-&gt;AssociatedIrp.SystemBuffer*是**NULL**，此成员必须为零。

<a href="" id="irpsp--parameters-create-fileattributes"></a>*IrpSp-&gt;Parameters.Create.FileAttributes*属性标志的位掩码，若要创建或打开文件时应用。 仅当创建、 被取代，或文件，在某些情况下，重写时，才应用显式指定的特性。 默认情况下，此值是文件\_特性\_正常，可以通过任何其他标志或兼容的标志或运算组合中重写。 此成员对应于*FileAttributes*参数[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)。

<a href="" id="irpsp--parameters-create-options"></a>*IrpSp-&gt;Parameters.Create.Options*标志，用于指定要创建或打开该文件，以及该文件已存在时要采取的操作时应用的选项的位掩码。

高的 8 位的此参数对应于*处置*参数[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)。

此成员的较低的 24 位对应于*CreateOptions*参数[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)。 文件系统筛选器和微筛选器驱动程序的执行 （如防病毒程序） 扫描文件需要特别注意到该文件\_完成\_如果\_OPLOCKED 标志。 如果设置此标志，该筛选器必须不阻止或否则延迟 IRP\_MJ\_创建操作。

如果该文件\_完成\_如果\_中 （创建调度） pre-create 设置 OPLOCKED 标志路径，该筛选器不能启动任何以下类型的操作，因为它们可能会导致 oplock 中断：

IRP\_MJ\_IRP 清理\_MJ\_创建 IRP\_MJ\_文件\_系统\_控制 IRP\_MJ\_刷新\_缓冲区 IRP\_MJ\_锁\_控制 IRP\_MJ\_读取的 IRP\_MJ\_设置\_信息 IRP\_MJ\_写入筛选器或微筛选器不会使用该文件\_完成\_IF\_OPLOCKED 标志，则必须完成 IRP\_MJ\_状态创建请求\_共享\_冲突。

如果该文件\_完成\_IF\_中完成设置 OPLOCKED 标志 （后创建） 路径，该筛选器应检查是否已设置的文件系统*Irp-&gt;IoStatus.Status*到状态\_OPLOCK\_中断\_IN\_进度状态值。 如果未设置此状态的值，则可以安全筛选器以启动对文件执行上述操作之一。 如果设置此状态的值，oplock 尚未尚未被中断，且筛选器不能启动的任何操作都可能会导致破坏 oplock。 因此筛选器必须推迟所有对文件执行上述操作直到以下条件之一为 true:

-   机会锁的所有者发送 FSCTL\_OPLOCK\_中断\_对文件系统的确认请求。
-   筛选器或微筛选器以外的系统组件发送的文件系统必须等待，直到需要破坏 oplock 已完成的 I/O 请求 (如 IRP\_MJ\_IRP 读\_MJ\_编写)。 筛选器或微筛选器可以启动一个对于此新操作，上述操作从其调度 （或 preoperation 回调） 例程，因为调度或 preoperation 回调例程会处于等待状态需要破坏 oplock 直到完成。

<a href="" id="irpsp--parameters-create-securitycontext--accessstate"></a>*IrpSp-&gt;Parameters.Create.SecurityContext-&gt;AccessState*指针，指向[**访问\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)包含对象的结构使用者上下文、 授予的访问类型和剩余所需访问类型。

<a href="" id="irpsp--parameters-create-securitycontext--desiredaccess"></a>*IrpSp-&gt;Parameters.Create.SecurityContext-&gt;DesiredAccess*访问\_掩码结构，它指定为文件请求的访问权限。 有关详细信息，请参阅的说明*DesiredAccess*参数[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)。

<a href="" id="irpsp--parameters-create-shareaccess"></a>*IrpSp-&gt;Parameters.Create.ShareAccess*文件要求的共享访问权限的位掩码。 如果此成员为零，正在请求独占访问权限。 有关详细信息，请参阅的说明*ShareAccess*参数[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)。

## <a name="see-also"></a>请参阅


[**ACCESS\_MASK**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[**ACCESS\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)

[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen)

[**FltReissueSynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreissuesynchronousio)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocancelfileopen)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)

[**IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobject)

[**IoCreateStreamFileObjectLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_CLEANUP**](irp-mj-cleanup.md)

[**IRP\_MJ\_CLOSE**](irp-mj-close.md)

[**IRP\_MJ\_创建 （WDK 内核参考）** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)

[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile)

 

 







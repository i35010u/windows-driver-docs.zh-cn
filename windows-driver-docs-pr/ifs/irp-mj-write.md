---
title: IRP_MJ_WRITE
description: IRP_MJ_WRITE
ms.assetid: 8f16a579-1598-4f70-8d88-dfe877daec31
keywords:
- IRP_MJ_WRITE 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_WRITE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7a9867fb75d40cc8cba61375f0c07544fa0613d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375667"
---
# <a name="irpmjwrite"></a>IRP\_MJ\_WRITE


## <a name="when-sent"></a>发送时间


IRP\_MJ\_写入 I/O 管理器或文件系统驱动程序发送请求。 可以将发送此请求，例如，在用户模式应用程序具有如调用 Microsoft Win32 函数时**WriteFile**或当调用内核模式组件[ **ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile).

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取和解码以确定参数和次要函数代码的文件对象。

MDL 写入请求的文件系统应检查次要函数代码，以确定请求的操作。 以下是有效的次要函数代码，可以仅针对缓存的文件 I/O 使用：

- IRP\_MN\_完成

- IRP\_MN\_完成\_MDL

- IRP\_MN\_完成\_MDL\_DPC

- IRP\_MN\_压缩

- IRP\_MN\_DPC

- IRP\_MN\_MDL

- IRP\_MN\_MDL\_DPC

- IRP\_MN\_正常

有关如何处理此 IRP，研究 FASTFAT 示例包括 Windows Driver Kit (WDK) 中。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应执行任何所需的处理和，具体取决于筛选器的特性，处于已完成或失败 IRP，或将其传递到下一步低驱动程序堆栈上。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理创建请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  

指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  

指向要用作中间系统缓冲区，如果系统提供缓冲区的指针是否\_缓冲\_中设置了 IO 标志*DeviceObject-&gt;标志*。 否则，此成员设置为**NULL**。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  

一个指向[ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)接收最终完成状态以及有关请求的操作信息的结构。 如果 IRP\_MJ\_写入请求失败，则文件系统写入调度例程将返回错误 NTSTATUS 值和的值*Irp-&gt;IoStatus.Information*未定义，不应为使用。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  

介绍数据是要写入的页面的内存描述符列表 (MDL) 的地址。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*

指向与关联的文件对象的指针*DeviceObject*。 如果 FO\_同步\_中设置了 IO 标志*IrpSp-&gt;的文件对象-&gt;标志*，为同步 I/O 打开文件对象。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_编写和不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;Flags*  

如果 SL\_FORCE\_直接\_设置写入标记、 内核模式驱动程序可以写入到卷区域，它们通常不能编写由于直接编写阻塞。 直接写阻塞是出于安全原因，Windows Vista 和更高版本操作系统中实现的。 在文件系统层和存储堆栈层检查此标志。 有关直接写阻止的详细信息，请参阅[阻止直接写入操作的卷和磁盘到](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 SL\_FORCE\_直接\_编写标志是在 Windows Vista 和更高版本的 Windows 中可用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*

指定 IRP\_MJ\_编写。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  

指定所请求的操作，并包含以下项之一：

-   IRP\_MN\_完成

-   IRP\_MN\_完成\_MDL

-   IRP\_MN\_完成\_MDL\_DPC

-   IRP\_MN\_压缩

-   IRP\_MN\_DPC

-   IRP\_MN\_MDL

-   IRP\_MN\_MDL\_DPC

-   IRP\_MN\_正常

<a href="" id="irpsp--parameters-write-byteoffset"></a>*IrpSp-&gt;Parameters.Write.ByteOffset*  

大型\_整数变量，用于指定要写入的数据文件中的起始字节偏移量。

在某些情况下，此参数可能包含一个特殊值。 例如：

-   如果以下条件为 true，则表明当前文件尾，应使用而不是显式文件偏移量值：

    *IrpSp-&gt;Parameters.Write.ByteOffset.LowPart* = = 文件\_编写\_TO\_最终\_OF\_文件并*IrpSp-&gt;Parameters.Write.ByteOffset.HighPart* = =-1

<a href="" id="irpsp--parameters-write-key"></a>*IrpSp-&gt;Parameters.Write.Key*  

目标文件的字节范围锁与关联的密钥值。

<a href="" id="irpsp--parameters-write-length"></a>*IrpSp-&gt;Parameters.Write.Length*  

要写入的数据长度以字节为单位。 如果写入操作成功，在返回写入的字节数**信息**成员的 IO\_状态\_指向块结构*Irp-&gt;IoStatus*.

<a name="remarks"></a>备注
-------

文件系统舍入写入和读取最多的扇区大小的倍数的文件的末尾的基础的文件存储设备的操作。 在处理预读或预写操作时，筛选的分配，并且交换缓冲区需要舍入到的关联的设备的扇区大小的倍数的分配的缓冲区的大小。 如果未显示，请从基础文件系统传输数据的长度将超过分配的缓冲区的长度。 有关交换缓冲区的详细信息，请参阅[swapBuffers 微筛选器示例](https://go.microsoft.com/fwlink/p/?linkid=256055)。

## <a name="see-also"></a>请参阅


[**CcMdlWriteComplete**](https://msdn.microsoft.com/library/windows/hardware/ff539172)

[**CcPrepareMdlWrite**](https://msdn.microsoft.com/library/windows/hardware/ff539181)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_READ**](irp-mj-read.md)

[**IRP\_MJ\_写入 （WDK 内核参考）** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)

[**ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile)

 

 







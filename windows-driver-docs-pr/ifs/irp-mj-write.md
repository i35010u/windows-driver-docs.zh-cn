---
title: 'IRP_MJ_WRITE (IFS) '
description: IRP_MJ_WRITE
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
ms.openlocfilehash: 1ef81362f255cb15cb1b70fe0c415e3ff86f839c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819059"
---
# <a name="irp_mj_write-ifs"></a>IRP \_ MJ \_ 写入 (IFS) 


## <a name="when-sent"></a>发送时间


IRP \_ MJ \_ 写入请求由 I/o 管理器或文件系统驱动程序发送。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如 **WriteFile** ）或内核模式组件已调用 [**ZwWriteFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)时，可以发送此请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定参数和次要函数代码。

对于 MDL 写入请求，文件系统应检查次要函数代码以确定请求的操作。 下面是有效的次要函数代码，只能用于缓存的文件 i/o：

- IRP \_ MN \_ 完成

- IRP \_ MN \_ 完成 \_ MDL

- IRP \_ MN \_ 完成 \_ MDL \_ DPC

- IRP \_ MN \_ 压缩

- IRP \_ MN \_ DPC

- IRP \_ MN \_ MDL

- IRP \_ MN \_ MDL \_ DPC

- IRP \_ MN \_ 正常

有关如何处理此 IRP 的详细信息，请查看 Windows 驱动程序工具包 (WDK) 中包含的 FASTFAT 示例。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应执行任何所需的处理，并根据筛选器的性质，要么完成 IRP 还是使 IRP 失败，要么将其向下传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 *IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在进程创建请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  

指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt;AssociatedIrp.SystemBuffer*  

一个指针，指向系统提供的用于中间系统缓冲区的缓冲区（如果 \_ \_ 在 *DeviceObject &gt; 标志* 中设置了 "执行缓冲 IO" 标记）。 否则，此成员设置为 **NULL**。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  

指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。 如果 IRP \_ MJ \_ 写入请求失败，则文件系统的写入调度例程将返回错误 NTSTATUS 值，并且 *&gt; IoStatus* 的值是不确定的，因此不应使用。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; MdlAddress*  

内存描述符列表的地址 (MDL) 描述数据要写入到的页面。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*

指向与 *DeviceObject* 关联的文件对象的指针。 如果 \_ \_ 在 *IrpSp- &gt; &gt; FLAGS 标记* 中设置了 FO 同步 IO 标志，则会为同步 i/o 打开文件对象。

*IrpSp- &gt; FileObject* 参数包含指向 **RelatedFileObject** 字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 写入期间无效 \_ ，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp- &gt; 标志*  

如果设置了 SL \_ 强制 \_ 直接 \_ 写入标志，则内核模式驱动程序可以写入通常因直接写入阻止而无法写入的卷区域。 出于安全原因，在 Windows Vista 和更高版本的操作系统中实现了直接写入阻止。 在文件系统层和存储堆栈层均检查此标志。 有关直接写入阻止的详细信息，请参阅 [阻止对卷和磁盘进行直接写入操作](/windows-hardware/drivers/ddi/index)。 SL \_ 强制 \_ 直接 \_ 写入标志在 windows Vista 和更高版本的 windows 中可用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*

指定 IRP \_ MJ \_ 写入。

<a href="" id="irpsp--minorfunction"></a>*IrpSp- &gt; MinorFunction*  

指定所请求的操作并包含以下项之一：

-   IRP \_ MN \_ 完成

-   IRP \_ MN \_ 完成 \_ MDL

-   IRP \_ MN \_ 完成 \_ MDL \_ DPC

-   IRP \_ MN \_ 压缩

-   IRP \_ MN \_ DPC

-   IRP \_ MN \_ MDL

-   IRP \_ MN \_ MDL \_ DPC

-   IRP \_ MN \_ 正常

<a href="" id="irpsp--parameters-write-byteoffset"></a>*IrpSp. &gt; ByteOffset*  

一个大 \_ 整数变量，它指定要写入的数据在文件中的起始字节偏移量。

在某些情况下，此参数可能包含一个特殊值。 例如：

-   如果以下条件为 true，则表示应使用当前文件结尾，而不是显式文件偏移值：

    *IrpSp- &gt;ByteOffset. LowPart* = = file \_ 写入 \_ \_ \_ 文件结尾 \_ 和 *IrpSp。 &gt; ByteOffset. largeint.highpart* = =-1

<a href="" id="irpsp--parameters-write-key"></a>*IrpSp- &gt; Parameters. Key*  

与目标文件的字节范围锁关联的键值。

<a href="" id="irpsp--parameters-write-length"></a>*IrpSp- &gt; Length*  

要写入的数据的长度（以字节为单位）。 如果写入操作成功，则会在 **Information** \_ \_ *&gt; IoStatus* 所指向的 IO 状态块结构的信息成员中返回写入的字节数。

<a name="remarks"></a>备注
-------

文件系统在文件末尾将写入和读取操作舍入到基础文件存储设备的多个扇区大小。 处理预读或预写入操作时，分配和交换缓冲区的筛选器需要将已分配缓冲区的大小舍入到关联设备的扇区大小的倍数。 否则，从基础文件系统传输的数据的长度将超过缓冲区的分配长度。 有关交换缓冲区的详细信息，请参阅 [SwapBuffers 微筛选器示例](/samples/browse/)。

## <a name="see-also"></a>请参阅


[**CcMdlWriteComplete**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccmdlwritecomplete)

[**CcPrepareMdlWrite**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccpreparemdlwrite)

[**FLT \_ IO \_ 参数 \_ 块**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 读取**](irp-mj-read.md)

[**IRP \_ MJ \_ 写入 (WDK 内核引用)**](../kernel/irp-mj-write.md)

[**ZwWriteFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)


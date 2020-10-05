---
title: 'IRP_MJ_READ (IFS) '
description: IRP_MJ_READ
ms.assetid: f2f909ff-4af6-433e-9f3c-9692b5ab7171
keywords:
- IRP_MJ_READ 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_READ
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 616a4acc23ac1941a8af654030e9d032d6d26629
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734277"
---
# <a name="irp_mj_read-ifs"></a>IRP \_ MJ \_ 读取 (IFS) 


## <a name="when-sent"></a>发送时间


IRP \_ MJ \_ 读取请求由 I/o 管理器或文件系统驱动程序发送。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如 **ReadFile**）或内核模式组件已调用 [**ZwReadFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)时，可以发送此请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定参数和次要函数代码。

 (MDL) 读取请求的内存描述符列表，则文件系统应检查次要函数代码以确定请求的操作。 下面是有效的次要函数代码，只能用于缓存的文件 i/o：

- IRP \_ MN \_ 完成

- IRP \_ MN \_ 完成 \_ MDL

- IRP \_ MN \_ 完成 \_ MDL \_ DPC

- IRP \_ MN \_ 压缩

- IRP \_ MN \_ DPC

- IRP \_ MN \_ MDL

- IRP \_ MN \_ MDL \_ DPC

- IRP \_ MN \_ 正常

有关处理此 IRP 的详细信息，请学习 (WDK) 中包含的 CDFS 和 FASTFAT 示例。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应执行任何所需的处理，并根据筛选器的性质，要么完成 IRP 还是使 IRP 失败，要么将 IRP 向下传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用 irp 的以下成员中包含的信息和 irp 堆栈位置来处理读取请求：

<a href="" id="deviceobject"></a>*DeviceObject*  

指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt;AssociatedIrp.SystemBuffer*  

一个指针，指向系统提供的用于中间系统缓冲区的缓冲区（如果 \_ \_ 在 *DeviceObject &gt; 标志*中设置了 "执行缓冲 IO" 标记）。 否则，此成员设置为 **NULL**。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  

指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。 有关详细信息，请参阅[**ZwReadFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)的*IoStatusBlock*参数说明。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; MdlAddress*  

 (MDL 的内存描述符列表的地址) 描述包含要读取的数据的页面。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  

指向调用方提供的输出缓冲区的指针，该缓冲区接收从该文件读取的数据。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  

指向与 *DeviceObject*关联的文件对象的指针。 如果 \_ \_ 在 *IrpSp- &gt; &gt; FLAGS 标记*中设置了 FO 同步 IO 标志，则会为同步 i/o 打开文件对象。

*IrpSp- &gt; FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 读取期间无效 \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  

指定 IRP \_ MJ \_ 读取。

<a href="" id="irpsp--minorfunction"></a>*IrpSp- &gt; MinorFunction*  

指定所请求的操作并包含以下项之一：

- IRP \_ MN \_ 完成

- IRP \_ MN \_ 完成 \_ MDL

- IRP \_ MN \_ 完成 \_ MDL \_ DPC

- IRP \_ MN \_ 压缩

- IRP \_ MN \_ DPC

- IRP \_ MN \_ MDL

- IRP \_ MN \_ MDL \_ DPC

- IRP \_ MN \_ 正常

<a href="" id="irpsp--parameters-read-byteoffset"></a>*IrpSp. &gt; ByteOffset*

一个大 \_ 整数变量，指定要读取的数据在文件中的起始字节偏移量。

<a href="" id="irpsp--parameters-read-key"></a>*IrpSp- &gt; Parameters。*

与目标文件的字节范围锁关联的键值。

<a href="" id="irpsp--parameters-read-length"></a>*IrpSp- &gt; Parameters*

要读取的数据的长度（以字节为单位）。 如果读取操作成功，则会在* &gt; IoStatus*所指向的[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构的**信息**成员中返回读取的字节数。

<a name="remarks"></a>备注
-------

文件系统在文件末尾将写入和读取操作舍入到基础文件存储设备的多个扇区大小。 处理预读或预写入操作时，分配和交换缓冲区的筛选器需要将已分配缓冲区的大小舍入到关联设备的扇区大小的倍数。 否则，从基础文件系统传输的数据的长度将超过缓冲区的分配长度。 有关交换缓冲区的详细信息，请参阅 [SwapBuffers 微筛选器示例](/samples/browse/)。

## <a name="see-also"></a>另请参阅


[**CcMdlRead**](/previous-versions/ff539159(v=vs.85))

[**CcMdlReadComplete**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ccmdlreadcomplete)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 读取 (WDK 内核参考) **](../kernel/irp-mj-read.md)

[**IRP \_ MJ \_ 写入**](irp-mj-write.md)

[**ZwReadFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)


---
title: IRP_MJ_READ
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
ms.openlocfilehash: cf7a790767107a310c53e531f18477aedd587a2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520391"
---
# <a name="irpmjread"></a>IRP\_MJ\_READ


## <a name="when-sent"></a>发送时间


IRP\_MJ\_读取 I/O 管理器或文件系统驱动程序发送请求。 可以将发送此请求，例如，在用户模式应用程序具有如调用 Microsoft Win32 函数时**ReadFile**，或当调用内核模式组件[ **ZwReadFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567072).

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取和解码以确定参数和次要函数代码的文件对象。

有关内存描述符列表 (MDL) 读取请求，文件系统应检查次要函数代码，以确定请求的操作。 以下是有效的次要函数代码，可以仅针对缓存的文件 I/O 使用：

- IRP\_MN\_完成

- IRP\_MN\_完成\_MDL

- IRP\_MN\_完成\_MDL\_DPC

- IRP\_MN\_压缩

- IRP\_MN\_DPC

- IRP\_MN\_MDL

- IRP\_MN\_MDL\_DPC

- IRP\_MN\_正常

有关处理此 IRP，研究 Windows Driver Kit (WDK) 中包含 CDFS 和 FASTFAT 示例。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应执行任何所需的处理和，具体取决于筛选器的特性，处于已完成或失败 IRP 或将其传递到下一步低驱动程序堆栈上。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和 IRP 堆栈位置在处理读取的请求中包含的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  

指向目标设备对象指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  

指向要用作中间系统缓冲区，如果系统提供缓冲区的指针是否\_缓冲\_中设置了 IO 标志*DeviceObject-&gt;标志*。 否则，此成员设置为**NULL**。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  

指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)接收最终完成状态以及有关请求的操作信息的结构。 有关详细信息，请参阅的说明*IoStatusBlock*参数[ **ZwReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff567072)。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  

描述包含要读取的数据的页内存描述符列表 (MDL) 的地址。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  

指向接收从文件读取数据的调用方提供输出缓冲区的指针。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  

与之关联的文件对象的指针*DeviceObject*。 如果 FO\_同步\_中设置了 IO 标志*IrpSp-&gt;的文件对象-&gt;标志*，为同步 I/O 打开文件对象。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_读取，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  

指定 IRP\_MJ\_读取。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  

指定所请求的操作，并包含以下项之一：

- IRP\_MN\_完成

- IRP\_MN\_完成\_MDL

- IRP\_MN\_完成\_MDL\_DPC

- IRP\_MN\_压缩

- IRP\_MN\_DPC

- IRP\_MN\_MDL

- IRP\_MN\_MDL\_DPC

- IRP\_MN\_正常

<a href="" id="irpsp--parameters-read-byteoffset"></a>*IrpSp-&gt;Parameters.Read.ByteOffset*

大型\_整数变量，用于指定要读取的数据文件中的起始字节偏移量。

<a href="" id="irpsp--parameters-read-key"></a>*IrpSp-&gt;Parameters.Read.Key*

目标文件的字节范围锁与关联的密钥值。

<a href="" id="irpsp--parameters-read-length"></a>*IrpSp-&gt;Parameters.Read.Length*

要读取的数据长度以字节为单位。 如果读取的操作成功，在返回读取的字节数**信息**的成员[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)指向结构*Irp-&gt;IoStatus*。

<a name="remarks"></a>备注
-------

文件系统舍入写入和读取最多的扇区大小的倍数的文件的末尾的基础的文件存储设备的操作。 在处理预读或预写操作时，筛选的分配，并且交换缓冲区需要舍入到的关联的设备的扇区大小的倍数的分配的缓冲区的大小。 如果未显示，请从基础文件系统传输数据的长度将超过分配的缓冲区的长度。 有关交换缓冲区的详细信息，请参阅[swapBuffers 微筛选器示例](https://go.microsoft.com/fwlink/p/?linkid=256055)。

## <a name="see-also"></a>另请参阅


[**CcMdlRead**](https://msdn.microsoft.com/library/windows/hardware/ff539159)

[**CcMdlReadComplete**](https://msdn.microsoft.com/library/windows/hardware/ff539163)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_读取 （WDK 内核参考）**](https://msdn.microsoft.com/library/windows/hardware/ff550794)

[**IRP\_MJ\_WRITE**](irp-mj-write.md)

[**ZwReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff567072)

 

 







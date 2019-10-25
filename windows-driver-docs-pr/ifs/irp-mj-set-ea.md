---
title: IRP_MJ_SET_EA
description: IRP\_MJ\_集\_EA
ms.assetid: f9e1f867-a473-46ac-a1c0-63534c4c0755
keywords:
- IRP_MJ_SET_EA 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_SET_EA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 156e45f78295dd5b1c42cbee234c92bdb7f3f6fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841153"
---
# <a name="irp_mj_set_ea"></a>IRP\_MJ\_集\_EA


## <a name="when-sent"></a>发送时间


I/o 管理器发送 IRP\_MJ\_集\_EA 请求来设置文件的扩展属性。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果文件系统支持扩展属性，则文件系统驱动程序应处理请求并完成 IRP。 否则，文件系统驱动程序应返回**状态\_EAS\_不\_支持**。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，以及在处理 set 扩展属性请求中的 IRP 堆栈位置：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp. SystemBuffer*  
指向系统提供的输入缓冲区的指针，该缓冲区包含要设置的扩展属性信息。 用于\_缓冲 i/o 的方法。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
描述接收扩展属性信息的输入缓冲区的内存描述符列表（MDL）的地址。 用于方法\_直接 i/o。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向调用方提供的[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构化输入缓冲区的指针，该缓冲区接收扩展属性信息。 用于方法\_i/o。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_设置\_EA 时无效，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定\_MJ\_集\_EA。

<a href="" id="irpsp--parameters-setea-length"></a>*IrpSp-&gt;参数. SetEa. 长度*  
输入缓冲区的长度（以字节为单位）。

## <a name="see-also"></a>另请参阅


[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_QUERY\_EA**](irp-mj-query-ea.md)

 

 







---
title: IRP_MJ_SET_EA
description: IRP \_ MJ \_ 设置 \_ EA
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
ms.openlocfilehash: e0da3bc48ec73ee9e005d816a9d7fc9ab41bbfa7
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066172"
---
# <a name="irp_mj_set_ea"></a>IRP \_ MJ \_ 设置 \_ EA


## <a name="when-sent"></a>发送时间


I/o 管理器发送 IRP \_ MJ \_ set \_ EA 请求，以设置文件的扩展属性。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果文件系统支持扩展属性，则文件系统驱动程序应处理请求并完成 IRP。 否则，文件系统驱动程序将返回 ** \_ \_ 不 \_ 受支持的状态 EAS**。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>parameters


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理 set 扩展属性请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt;AssociatedIrp.SystemBuffer*  
指向系统提供的输入缓冲区的指针，该缓冲区包含要设置的扩展属性信息。 用于方法 \_ 缓冲 i/o。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; MdlAddress*  
 (MDL 的内存描述符列表的地址) 描述接收扩展属性信息的输入缓冲区。 用于方法 \_ 直接 i/o。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
指向调用方提供的 [**文件 \_ 完整 \_ EA \_ information**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构化输入缓冲区的指针，该缓冲区接收扩展属性信息。 用于方法 \_ 不是 i/o。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
指向与 *DeviceObject*关联的文件对象的指针。

*IrpSp- &gt; FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 集 EA 期间无效 \_ \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 集 \_ EA。

<a href="" id="irpsp--parameters-setea-length"></a>*IrpSp- &gt; SetEa. Length*  
输入缓冲区的长度（以字节为单位）。

## <a name="see-also"></a>请参阅


[**文件 \_ 完整的 \_ EA \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 查询 \_ EA**](irp-mj-query-ea.md)

 


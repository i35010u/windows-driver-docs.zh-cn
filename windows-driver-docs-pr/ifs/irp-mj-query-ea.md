---
title: IRP_MJ_QUERY_EA
description: IRP \_ MJ \_ 查询 \_ EA
keywords:
- IRP_MJ_QUERY_EA 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_EA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3e837a8f56518aecde7ff6dce6e96aab5e8b9f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819063"
---
# <a name="irp_mj_query_ea"></a>IRP \_ MJ \_ 查询 \_ EA


## <a name="when-sent"></a>发送时间


在 \_ \_ \_ 用户模式应用程序请求了有关文件的扩展属性的信息时，由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送 IRP MJ 查询 EA 请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果文件系统支持扩展属性，则文件系统驱动程序应处理查询并完成 IRP。 否则，不支持返回状态 \_ EAS \_ \_ 。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 *IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理 irp \_ MJ \_ 查询 EA 请求中的以下 irp 成员和 irp 堆栈位置设置的信息 \_ ：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt;AssociatedIrp.SystemBuffer*  
指向系统提供的输出缓冲区的指针，该缓冲区用作中间系统缓冲区。 用于方法 \_ 缓冲 i/o。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; MdlAddress*  
 (MDL 的内存描述符列表的地址) 描述接收扩展属性信息的输出缓冲区。 用于方法 \_ 直接 i/o。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
指向调用方提供的 [**文件完整的 \_ \_ EA \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构化输出缓冲区的指针，该缓冲区接收扩展属性信息。 用于方法 \_ 不是 i/o。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
指向与 *DeviceObject* 关联的文件对象的指针。

*IrpSp- &gt; FileObject* 参数包含指向 **RelatedFileObject** 字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 查询 EA 期间无效 \_ \_ ，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp- &gt; 标志*  
指定以下一个或多个值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_INDEX_SPECIFIED</p></td>
<td align="left"><p>在扩展属性列表中的条目开始扫描，其索引由 <em>IrpSp &gt; QueryEa. EaIndex</em>提供。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>从列表中的第一个条目开始扫描。 如果未设置此标志，则从上一个 IRP_MJ_QUERY_EA 请求恢复扫描。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>仅返回找到的第一个条目。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 查询 \_ EA。

<a href="" id="irpsp--parameters-queryea-eaindex"></a>*IrpSp- &gt; QueryEa. EaIndex*  
开始扫描扩展属性列表的项的索引。 如果 \_ \_ 未设置 SL 索引指定标志，或者如果 *IrpSp &gt; QueryEa* 指向非空列表，则忽略此参数。

<a href="" id="irpsp--parameters-queryea-ealist"></a>*IrpSp- &gt; QueryEa. EaList*  
指向调用方提供的文件的 [**指针 \_ 获取 \_ EA \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_ea_information)结构化输入缓冲区，并指定要查询的扩展属性。

<a href="" id="irpsp--parameters-queryea-ealistlength"></a>*IrpSp- &gt; QueryEa. EaListLength*  
IrpSp 所指向的缓冲区的长度（以字节为单位） *&gt; 。 QueryEa. EaList*。

<a href="" id="irpsp--parameters-queryea-length"></a>*IrpSp- &gt; QueryEa. Length*  
输出缓冲区的长度（以字节为单位）。

<a name="remarks"></a>备注
-------

如果提供了短缓冲区并且返回了状态 \_ 缓冲区 \_ 溢出，则 NTFS 将返回最新的 \_ 完整 \_ EA information \_ 条目。 如果提供了短缓冲区并且返回了状态 \_ 缓冲区 \_ 太 \_ 小，则 NTFS 无法容纳任何文件的 \_ 完整 \_ EA \_ 信息条目。

> [!NOTE]
> 在 Windows Vista 和更高版本中，FAT16 不再支持扩展属性。

 

## <a name="see-also"></a>请参阅


[**文件 \_ 完整的 \_ EA \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**文件 \_ 获取 \_ EA \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_ea_information)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 设置 \_ EA**](irp-mj-set-ea.md)

 


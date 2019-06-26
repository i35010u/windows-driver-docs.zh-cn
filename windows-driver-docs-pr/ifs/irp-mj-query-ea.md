---
title: IRP_MJ_QUERY_EA
description: IRP\_MJ\_查询\_EA
ms.assetid: 5d60a6e9-e940-44cf-844b-86837b36237a
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
ms.openlocfilehash: d4905b75dbe9e7164230510a312dd3bcf0a0442e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384820"
---
# <a name="irpmjqueryea"></a>IRP\_MJ\_查询\_EA


## <a name="when-sent"></a>发送时间


IRP\_MJ\_查询\_EA 发送请求 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序，在用户模式应用程序已请求文件有关的信息的扩展特性。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果文件系统支持扩展的属性，文件系统驱动程序应处理该查询，并完成 IRP。 否则，它应返回状态\_EAS\_不\_受支持。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理 IRP 的 IRP 堆栈位置中设置的信息\_MJ\_查询\_EA 请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
指向要用作中间系统缓冲区的系统提供的输出缓冲区的指针。 用于方法\_缓冲 I/O。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
一个指向[ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
内存描述符列表 (MDL) 描述接收的扩展的属性信息的输出缓冲区的地址。 用于方法\_直接 I/O。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向调用方提供的指针[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)-接收的扩展的属性信息的结构化的输出缓冲区。 用于方法\_既不 I/O。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_查询\_EA 和不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;Flags*  
指定一个或多个以下值。

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
<td align="left"><p>SL_INDEX_SPECIFIED</p></td>
<td align="left"><p>开始在给定其索引的扩展的属性列表中的条目扫描<em>IrpSp-&gt;Parameters.QueryEa.EaIndex</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>开始在列表中的第一个条目扫描。 如果未设置此标志，继续从上一个 IRP_MJ_QUERY_EA 请求扫描。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>返回只找到的第一个条目。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_查询\_EA。

<a href="" id="irpsp--parameters-queryea-eaindex"></a>*IrpSp-&gt;Parameters.QueryEa.EaIndex*  
在其开始扫描的扩展属性列表项的索引。 如果忽略此参数 SL\_索引\_未设置指定标志或如果*IrpSp-&gt;Parameters.QueryEa.EaList*指向非空列表。

<a href="" id="irpsp--parameters-queryea-ealist"></a>*IrpSp-&gt;Parameters.QueryEa.EaList*  
指向调用方提供的指针[**文件\_获取\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_get_ea_information)-指定要查询的扩展的属性的结构化输入的缓冲区。

<a href="" id="irpsp--parameters-queryea-ealistlength"></a>*IrpSp-&gt;Parameters.QueryEa.EaListLength*  
指向缓冲区的长度以字节为单位*IrpSp-&gt;Parameters.QueryEa.EaList*。

<a href="" id="irpsp--parameters-queryea-length"></a>*IrpSp-&gt;Parameters.QueryEa.Length*  
以字节为单位的输出缓冲区的长度。

<a name="remarks"></a>备注
-------

提供简短的缓冲区时，状态\_缓冲区\_返回溢出，NTFS 将返回最后一个整个文件\_完整\_EA\_适合的信息项。 提供简短的缓冲区时，状态\_缓冲区\_过\_返回较小，NTFS，无法容纳的任何文件\_完整\_EA\_信息条目。

&gt; \[!请注意\] &gt; FAT16 Windows Vista 及更高版本，不再支持扩展的属性。

 

## <a name="see-also"></a>请参阅


[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)

[**文件\_获取\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_get_ea_information)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_SET\_EA**](irp-mj-set-ea.md)

 

 







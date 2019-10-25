---
title: IRP_MJ_QUERY_EA
description: IRP\_MJ\_QUERY\_EA
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
ms.openlocfilehash: 2e40b69d0602c055d4522e31241dfdd92c643b52
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841169"
---
# <a name="irp_mj_query_ea"></a>IRP\_MJ\_QUERY\_EA


## <a name="when-sent"></a>发送时间


在用户模式应用程序请求了有关文件的扩展属性的信息时，由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送 IRP\_MJ\_查询\_EA 请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果文件系统支持扩展属性，则文件系统驱动程序应处理查询并完成 IRP。 否则，它应该返回状态\_EAS\_不\_支持。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用在处理 IRP\_MJ\_QUERY\_EA 请求中的以下 IRP 成员和 IRP 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp. SystemBuffer*  
指向系统提供的输出缓冲区的指针，该缓冲区用作中间系统缓冲区。 用于\_缓冲 i/o 的方法。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
描述接收扩展属性信息的输出缓冲区的内存描述符列表（MDL）的地址。 用于方法\_直接 i/o。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向调用方提供的[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构化输出缓冲区的指针，该缓冲区接收扩展属性信息。 用于方法\_i/o。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_查询\_EA 期间无效，不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;标志*  
指定以下一个或多个值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">旗帜</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_INDEX_SPECIFIED</p></td>
<td align="left"><p>在 "扩展属性" 列表中的条目开始扫描，其索引由&gt;IrpSp 指定，即<em>QueryEa. EaIndex</em>。</p></td>
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

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定\_MJ\_QUERY\_EA。

<a href="" id="irpsp--parameters-queryea-eaindex"></a>*IrpSp-&gt;参数. QueryEa. EaIndex*  
开始扫描扩展属性列表的项的索引。 如果未设置 SL\_索引\_指定标志，或者 *&gt;如果 QueryEa EaList*指向非空列表，则忽略此参数。

<a href="" id="irpsp--parameters-queryea-ealist"></a>*IrpSp-&gt;参数. QueryEa. EaList*  
指向调用方提供的文件的指针[ **\_获取\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_ea_information)结构化输入缓冲区来指定要查询的扩展属性。

<a href="" id="irpsp--parameters-queryea-ealistlength"></a>*IrpSp-&gt;参数. QueryEa. EaListLength*  
IrpSp 所指向的缓冲区的长度（以字节为单位） *&gt;QueryEa. EaList*。

<a href="" id="irpsp--parameters-queryea-length"></a>*IrpSp-&gt;参数. QueryEa. 长度*  
输出缓冲区的长度（以字节为单位）。

<a name="remarks"></a>备注
-------

如果提供了短缓冲区并且返回了状态\_缓冲区\_溢出，则 NTFS 返回\_完整\_EA\_信息条目中的最后一个完整文件。 如果提供了短缓冲区并且状态\_缓冲区\_\_小，则 NTFS 无法完全容纳所有文件\_完全\_的 EA\_信息条目。

&gt; \[！请注意\] Windows Vista 和更高版本上的 &gt;，FAT16 不再支持扩展属性。

 

## <a name="see-also"></a>另请参阅


[**文件\_完整\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**文件\_获取\_EA\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_get_ea_information)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_集\_EA**](irp-mj-set-ea.md)

 

 







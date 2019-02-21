---
title: IRP_MJ_QUERY_QUOTA
description: IRP\_MJ\_查询\_配额
ms.assetid: eb48b5ef-7eac-49d4-ab23-2d3efe783fa3
keywords:
- IRP_MJ_QUERY_QUOTA 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_QUOTA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c669dba96982735b99f9650fb180ea485aca60d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520395"
---
# <a name="irpmjqueryquota"></a>IRP\_MJ\_查询\_配额


## <a name="when-sent"></a>发送时间


IRP\_MJ\_查询\_配额请求发送的 I/O 管理器。 可以将发送此请求，例如，在用户模式应用程序具有如调用 Microsoft Win32 方法时**IDiskQuotaControl::GetQuotaState**。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


如果文件系统支持磁盘配额，应提取文件系统驱动程序并将其解码以确定它是否表示打开的文件或目录的用户的文件对象。 如果是这样，该驱动程序应处理该查询，并完成 IRP。 否则，驱动程序应完成根据 IRP，而不会处理该查询。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序，除非它需要显式重写配额行为。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理查询配额信息请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象指针。

<a href="" id="deviceobject--flags"></a>*DeviceObject-&gt;标志*  
DO\_缓冲\_IO 和 DO\_直接\_，如下所示使用 IO 标志来指定所依据的数据传递给驱动程序的方法：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志设置</th>
<th align="left">I/O 方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>~DO_BUFFERED_IO</p>
<p>&amp; ~DO_DIRECT_IO</p></td>
<td align="left"><p>METHOD_NEITHER</p></td>
</tr>
<tr class="even">
<td align="left"><p>~DO_BUFFERED_IO</p>
<p>&amp; DO_DIRECT_IO</p></td>
<td align="left"><p>METHOD_DIRECT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DO_BUFFERED_IO</p>
<p>&amp; ~DO_DIRECT_IO</p></td>
<td align="left"><p>METHOD_BUFFERED</p></td>
</tr>
<tr class="even">
<td align="left"><p>DO_BUFFERED_IO</p>
<p>&amp; DO_DIRECT_IO</p></td>
<td align="left"><p>METHOD_BUFFERED</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
指向要用作中间系统缓冲区，如果系统提供缓冲区的指针是否\_缓冲\_中设置了 IO 标志*DeviceObject-&gt;标志*。 否则，此成员设置为**NULL**。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向调用方提供的文件指针\_配额\_接收该卷的配额信息的结构信息的输出缓冲区。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
与之关联的文件对象的指针*DeviceObject*。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_查询\_配额并不应使用。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;Flags*  
此成员可以是一个或多项操作：

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
<td align="left"><p>开始在其索引由给定的配额列表中的条目扫描<em>IrpSp-&gt;Parameters.QueryQuota.StartSid</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_RESTART_SCAN</p></td>
<td align="left"><p>开始在列表中的第一个条目扫描。 如果未设置此标志，继续从上一个 IRP_MJ_QUERY_QUOTA 请求扫描。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SL_RETURN_SINGLE_ENTRY</p></td>
<td align="left"><p>返回只找到的第一个条目。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_查询\_配额。

<a href="" id="irpsp--parameters-queryquota-length"></a>*IrpSp-&gt;Parameters.QueryQuota.Length*  
指向缓冲区的长度，以字节为单位， *Irp-&gt;UserBuffer*。

<a href="" id="irpsp--parameters-queryquota-sidlist"></a>*IrpSp-&gt;Parameters.QueryQuota.SidList*  
可选指向其配额信息是要返回的 Sid 的列表。 在列表中的每个条目是[**文件\_获取\_配额\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540298)结构。 此结构定义，如下所示：

```cpp
typedef struct _FILE_GET_QUOTA_INFORMATION {
    ULONG NextEntryOffset;
    ULONG SidLength;
    SID Sid;
} FILE_GET_QUOTA_INFORMATION, *PFILE_GET_QUOTA_INFORMATION;
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NextEntryOffset</strong></p></td>
<td align="left"><p>下一步 FILE_GET_QUOTA_INFORMATION 条目，如果多个条目都位于一个缓冲区的字节偏移量。 如果没有其他项遵循这一属性，此成员为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SidLength</strong></p></td>
<td align="left"><p>长度 （字节） 的<strong>Sid</strong>成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Sid</strong></p></td>
<td align="left"><p>安全标识符 (SID)。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-queryquota-sidlistlength"></a>*IrpSp-&gt;Parameters.QueryQuota.SidListLength*  
指定的 Sid，如果一个列表的长度，以字节为单位。

<a href="" id="irpsp--parameters-queryquota-startsid"></a>*IrpSp-&gt;Parameters.QueryQuota.StartSid*  
指示返回的信息是第一个以外的条目启动一个 SID 到的可选指针。 如果指定 SID 列表，则忽略此参数。

## <a name="see-also"></a>另请参阅


[**文件\_获取\_配额\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540298)

[**文件\_配额\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540342)

[**IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoCheckQuotaBufferValidity**](https://msdn.microsoft.com/library/windows/hardware/ff548279)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_SET\_QUOTA**](irp-mj-set-quota.md)

 

 







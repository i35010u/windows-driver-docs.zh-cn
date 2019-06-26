---
title: IRP_MJ_QUERY_SECURITY
description: IRP\_MJ\_查询\_安全
ms.assetid: f0f73bfe-c016-49e2-b725-380f46a9b9d6
keywords:
- IRP_MJ_QUERY_SECURITY 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_SECURITY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41565840b369e238c2af27929b49c1a603d5de1d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384805"
---
# <a name="irpmjquerysecurity"></a>IRP\_MJ\_查询\_安全


## <a name="when-sent"></a>发送时间


IRP\_MJ\_查询\_安全请求将发送的 I/O 管理器。 它可以发送，例如，在用户模式应用程序具有如调用 Microsoft Win32 函数时**GetSecurityInfo**。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取和解码以确定是否表示用户文件或目录打开的文件对象。 如果是这样，该驱动程序应处理该查询，并完成 IRP。 否则，驱动程序应完成根据 IRP，而不会处理该查询。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应在堆栈上传递此 IRP 到下一步低驱动程序。

## <a name="parameters"></a>Parameters


文件系统或筛选器驱动程序调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)与给定 IRP，若要获取一个指向其自己[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)中，在以下列表中所示*IrpSp*。 (显示为 IRP *Irp*。)该驱动程序可以使用以下成员的 IRP 和在处理查询安全请求的 IRP 堆栈位置中设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
一个指向[ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)接收最终完成状态以及有关请求的操作信息的结构。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向接收副本的指定对象的安全描述符的调用方提供输出缓冲区的指针。 调用进程必须有权查看对象的安全状态的指定的方面。 [**安全\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))自相关格式返回结构。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与关联的文件对象的指针*DeviceObject*。

Windows XP 及更高版本，文件对象可以表示命名的数据流。 有关命名的数据流的详细信息，请参阅[**文件\_流\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stream_information)。

*IrpSp-&gt;的文件对象*参数包含一个指向**RelatedFileObject**字段中，这也是一个文件\_对象结构。 **RelatedFileObject**字段的文件\_对象结构不是有效的 IRP 处理期间\_MJ\_查询\_安全和不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_查询\_安全。

<a href="" id="irpsp--parameters-querysecurity-length"></a>*IrpSp-&gt;Parameters.QuerySecurity.Length*  
大小 （字节） 通过指向的缓冲区*Irp-&gt;UserBuffer*参数。

<a href="" id="irpsp--parameters-querysecurity-securityinformation"></a>*IrpSp-&gt;Parameters.QuerySecurity.SecurityInformation*  
一个指向[**安全\_信息**](security-information.md)操作结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SecurityInformation 值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在查询的对象的所有者标识符。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在查询的对象的主要组标识符。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在查询的对象的自由访问控制列表 (DACL)。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在查询的对象的系统 ACL (SACL)。 需要 ACCESS_SYSTEM_SECURITY 访问权限。</p></td>
</tr>
</tbody>
</table>

 

## <a name="see-also"></a>请参阅


[**文件\_流\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stream_information)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_SET\_SECURITY**](irp-mj-set-security.md)

[**安全\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**安全\_信息**](security-information.md)

 

 







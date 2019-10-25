---
title: IRP_MJ_QUERY_SECURITY
description: IRP\_MJ\_QUERY\_安全性
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
ms.openlocfilehash: a5793729095fb4a95787e78ce6b78e894728a42f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841163"
---
# <a name="irp_mj_query_security"></a>IRP\_MJ\_QUERY\_安全性


## <a name="when-sent"></a>发送时间


IRP\_MJ\_QUERY\_SECURITY 请求由 i/o 管理器发送。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如**GetSecurityInfo**）时，可以将其发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定它是表示用户文件还是打开目录。 如果是这样，则驱动程序应处理查询并完成 IRP。 否则，驱动程序应视需要完成 IRP，而不处理查询。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理查询安全请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
指向[**IO\_状态的指针\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构，它接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
指向调用方提供的输出缓冲区的指针，该缓冲区接收指定对象的安全描述符的副本。 调用进程必须具有查看对象安全状态的指定方面的权限。 [**安全\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))结构以自相关格式返回。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

在 Windows XP 和更高版本中，文件对象可以表示命名的数据流。 有关命名数据流的详细信息，请参阅[**FILE\_STREAM\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)。

*&gt;IrpSp FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件\_对象结构。 文件\_对象结构的**RelatedFileObject**字段在处理 IRP\_MJ\_查询\_安全性时无效，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
指定 IRP\_MJ\_QUERY\_SECURITY。

<a href="" id="irpsp--parameters-querysecurity-length"></a>*IrpSp-&gt;参数. QuerySecurity. 长度*  
*Irp&gt;UserBuffer*参数指向的缓冲区的大小（以字节为单位）。

<a href="" id="irpsp--parameters-querysecurity-securityinformation"></a>*IrpSp-&gt;参数. QuerySecurity. SecurityInformation*  
一个指针，指向操作的[**安全\_信息**](security-information.md)结构。

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
<td align="left"><p>指示正在查询对象的所有者标识符。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在查询对象的主要组标识符。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在查询对象的自由访问控制列表（DACL）。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在查询对象的系统 ACL （SACL）。 需要 ACCESS_SYSTEM_SECURITY 访问权限。</p></td>
</tr>
</tbody>
</table>

 

## <a name="see-also"></a>另请参阅


[**文件\_流\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_集\_安全性**](irp-mj-set-security.md)

[**安全\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**安全\_信息**](security-information.md)

 

 







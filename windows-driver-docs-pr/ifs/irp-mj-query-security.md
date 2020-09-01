---
title: IRP_MJ_QUERY_SECURITY
description: IRP \_ MJ \_ 查询 \_ 安全性
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
ms.openlocfilehash: a84ae5ae6478d4f7b7fbc5788e6dc07192f04123
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066180"
---
# <a name="irp_mj_query_security"></a>IRP \_ MJ \_ 查询 \_ 安全性


## <a name="when-sent"></a>发送时间


IRP \_ MJ \_ QUERY \_ SECURITY 请求由 i/o 管理器发送。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如 **GetSecurityInfo**）时，可以将其发送。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定它是表示用户文件还是打开目录。 如果是这样，则驱动程序应处理查询并完成 IRP。 否则，驱动程序应视需要完成 IRP，而不处理查询。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>parameters


文件系统或筛选器驱动程序与给定的 IRP 一起调用[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理 query security 请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
指向调用方提供的输出缓冲区的指针，该缓冲区接收指定对象的安全描述符的副本。 调用进程必须具有查看对象安全状态的指定方面的权限。 [**安全 \_ 描述符**](/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))结构以自相关格式返回。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
指向与 *DeviceObject*关联的文件对象的指针。

在 Windows XP 和更高版本中，文件对象可以表示命名的数据流。 有关命名数据流的详细信息，请参阅 [**文件 \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)。

*IrpSp- &gt; FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 查询安全性期间无效 \_ \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 查询 \_ 安全性。

<a href="" id="irpsp--parameters-querysecurity-length"></a>*IrpSp- &gt; QuerySecurity. Length*  
由 *Irp- &gt; UserBuffer* 参数指向的缓冲区的大小（以字节为单位）。

<a href="" id="irpsp--parameters-querysecurity-securityinformation"></a>*IrpSp- &gt; QuerySecurity. SecurityInformation*  
指向操作的 [**安全 \_ 信息**](security-information.md) 结构的指针。

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
<td align="left"><p>指示正在查询对象 (DACL) 的自由访问控制列表。 需要 READ_CONTROL 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在查询对象的系统 ACL (SACL) 。 需要 ACCESS_SYSTEM_SECURITY 访问权限。</p></td>
</tr>
</tbody>
</table>

 

## <a name="see-also"></a>请参阅


[**文件 \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 设置 \_ 安全性**](irp-mj-set-security.md)

[**安全 \_ 描述符**](/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**安全 \_ 信息**](security-information.md)

 


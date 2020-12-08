---
title: IRP_MJ_SET_SECURITY
description: IRP \_ MJ \_ 设置 \_ 安全性
keywords:
- IRP_MJ_SET_SECURITY 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_SET_SECURITY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a76e5e8d3ae2188371e5f68bb1a9053370b462ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793747"
---
# <a name="irp_mj_set_security"></a>IRP \_ MJ \_ 设置 \_ 安全性


## <a name="when-sent"></a>发送时间


IRP \_ MJ \_ SET \_ SECURITY 请求由 i/o 管理器发送。 例如，在用户模式应用程序调用 Win32 函数（如 **SetSecurityInfo**）时，可以发送此请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定它是表示用户文件还是打开目录。 如果是这样，则驱动程序应处理请求并完成 IRP。 否则，驱动程序应根据需要完成 IRP，而不处理请求。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 *IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理 set security information 请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
指向与 *DeviceObject* 关联的文件对象的指针。

*IrpSp- &gt; FileObject* 参数包含指向 **RelatedFileObject** 字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 集安全性期间无效 \_ \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 设置 \_ 安全性。

<a href="" id="irpsp--parameters-setsecurity-securitydescriptor"></a>*IrpSp- &gt; SetSecurity. SecurityDescriptor*  
指向 [**安全 \_ 描述符**](/previous-versions/windows/hardware/drivers/ff556610(v=vs.85)) 结构的指针，该结构包含要分配给对象的安全信息的值。

<a href="" id="irpsp--parameters-setsecurity-securityinformation"></a>*IrpSp- &gt; SetSecurity. SecurityInformation*  
类型为 " [**安全 \_ 信息**](security-information.md) " 的值，指定要在安全描述符中设置的安全信息。 此值可以是下列值之一。

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
<td align="left"><p>DACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在设置对象 (DACL) 的自由访问控制列表。 需要 WRITE_DAC 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GROUP_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在设置对象的主要组标识符。 需要 WRITE_OWNER 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OWNER_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在设置对象的所有者标识符。 需要 WRITE_OWNER 访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SACL_SECURITY_INFORMATION</p></td>
<td align="left"><p>指示正在设置对象的系统 ACL (SACL) 。 需要 ACCESS_SYSTEM_SECURITY 访问权限。</p></td>
</tr>
</tbody>
</table>

 

## <a name="see-also"></a>请参阅


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 查询 \_ 安全性**](irp-mj-query-security.md)

[**安全 \_ 描述符**](/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

[**安全 \_ 信息**](security-information.md)

 


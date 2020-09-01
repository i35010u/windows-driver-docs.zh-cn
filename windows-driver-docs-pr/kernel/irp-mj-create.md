---
title: IRP_MJ_CREATE
description: 每个内核模式驱动程序必须在 DispatchCreate 或 DispatchCreateClose 例程中处理 IRP_MJ_CREATE 请求。
ms.date: 08/12/2017
ms.assetid: 2947f8dc-2e7d-401e-8014-6140cac6905f
keywords:
- IRP_MJ_CREATE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 4a81355c994a5a11e37246d716a4efd48db620e4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188281"
---
# <a name="irp_mj_create"></a>IRP\_MJ\_CREATE


每个内核模式驱动程序必须在[*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数中处理**IRP \_ MJ \_ CREATE**请求。

<a name="when-sent"></a>发送时间
---------

操作系统将发送 **IRP \_ MJ \_ CREATE** 请求，以打开文件对象或设备对象的句柄。 例如，当驱动程序调用 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)时，操作系统将发送 **IRP \_ MJ \_ CREATE** 请求来执行实际的打开操作。

## <a name="input-parameters"></a>输入参数


**SecurityContext**成员指向某个[**IO \_ 安全 \_ 上下文**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_security_context)结构，该结构描述请求的安全上下文。 **SecurityContext- &gt; DesiredAccess**成员是一个访问掩码，它指定调用方请求的访问权限。

**参数. Create. Options**成员是一个 ULONG 值，用于描述在打开句柄时使用的选项。 高8位对应于**ZwCreateFile**的*CreateDisposition*参数的值，低24位对应于**ZwCreateFile**的*CreateOptions*参数的值。

**ShareAccess**成员是一个描述共享访问类型的 USHORT 值。 此值对应于**ZwCreateFile**的*ShareAccess*参数的值。

**FileAttributes**和**EaLength**成员保留供文件系统和文件系统筛选器驱动程序使用。 有关详细信息，请参阅可安装的文件系统 (IFS) 文档中的 [**IRP \_ MJ \_ 创建**](../ifs/irp-mj-create.md) 主题。

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

大多数设备和中间驱动程序 \_ 在 IRP 的 i/o 状态块中设置了状态 SUCCESS 并完成了创建请求，但驱动程序可以选择使用其 [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 回调函数为该句柄的任何后续 i/o 请求预留资源。 例如，系统序列驱动程序会映射其分页代码，并分配处理尝试打开设备以输入和输出的用户模式线程的后续 i/o 请求所需的任何资源。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchCreateClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IO \_ 安全 \_ 上下文**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_security_context)

[**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

 


---
title: IRP_MJ_CREATE
description: 每个内核模式驱动程序必须在 DispatchCreate 或 DispatchCreateClose 例程中处理 IRP_MJ_CREATE 请求。
ms.date: 08/12/2017
ms.assetid: 2947f8dc-2e7d-401e-8014-6140cac6905f
keywords:
- IRP_MJ_CREATE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 66c9f4346fd7c5fae0e8107e2e216f5c7f88015a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828126"
---
# <a name="irp_mj_create"></a>IRP\_MJ\_CREATE


每个内核模式驱动程序必须在[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数中处理**IRP\_MJ\_CREATE**请求。

<a name="when-sent"></a>发送时间
---------

操作系统将**IRP\_MJ 发送\_CREATE**请求，以打开文件对象或设备对象的句柄。 例如，当驱动程序调用[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)时，操作系统会发送**IRP\_MJ\_创建**请求来执行实际的打开操作。

## <a name="input-parameters"></a>输入参数


**SecurityContext**成员指向[**IO\_安全\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_security_context)结构，该结构描述请求的安全上下文。 **SecurityContext-&gt;DesiredAccess**成员是一个访问掩码，它指定调用方请求的访问权限。

**参数. Create. Options**成员是一个 ULONG 值，用于描述在打开句柄时使用的选项。 高8位对应于**ZwCreateFile**的*CreateDisposition*参数的值，低24位对应于**ZwCreateFile**的*CreateOptions*参数的值。

**ShareAccess**成员是一个描述共享访问类型的 USHORT 值。 此值对应于**ZwCreateFile**的*ShareAccess*参数的值。

**FileAttributes**和**EaLength**成员保留供文件系统和文件系统筛选器驱动程序使用。 有关详细信息，请参阅 "可安装文件系统（IFS）" 文档中的[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)主题。

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

大多数设备和中间驱动程序在 IRP 的 i/o 状态块中将状态设置\_成功，并完成了创建请求，但驱动程序可以选择使用其[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数为任何后续 i/o 保留资源针对该句柄的请求。 例如，系统序列驱动程序会映射其分页代码，并分配处理尝试打开设备以输入和输出的用户模式线程的后续 i/o 请求所需的任何资源。

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
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IO\_安全\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_security_context)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

 

 





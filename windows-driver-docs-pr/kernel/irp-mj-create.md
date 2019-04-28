---
title: IRP_MJ_CREATE
description: 每个内核模式驱动程序必须处理 IRP_MJ_CREATE DispatchCreate 或 DispatchCreateClose 例程中的请求。
ms.date: 08/12/2017
ms.assetid: 2947f8dc-2e7d-401e-8014-6140cac6905f
keywords:
- IRP_MJ_CREATE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 954c4a47fc9003f4aac13be33e0ba2a190ebfad4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351719"
---
# <a name="irpmjcreate"></a>IRP\_MJ\_CREATE


每个内核模式驱动程序必须处理**IRP\_MJ\_创建**中的请求[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)回调函数。

<a name="when-sent"></a>发送时间
---------

操作系统发送**IRP\_MJ\_创建**请求打开文件对象或设备对象的句柄。 例如，当驱动程序调用[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)，操作系统发送**IRP\_MJ\_创建**执行的实际请求打开操作。

## <a name="input-parameters"></a>输入参数


**Parameters.Create.SecurityContext**成员将指向[ **IO\_安全\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff550613)描述安全结构请求上下文。 **Parameters.Create.SecurityContext-&gt;DesiredAccess**成员是指定正在请求由调用方的访问权限的访问掩码。

**Parameters.Create.Options**成员是 ULONG 值，描述打开句柄时使用的选项。 高的 8 位的值对应*CreateDisposition*的参数**ZwCreateFile**，并与低 24 位对应的值*CreateOptions*参数**zwcreatefile 转换**。

**Parameters.Create.ShareAccess**成员是 USHORT 值，该值描述的共享访问权限的类型。 此值对应的值*ShareAccess*的参数**ZwCreateFile**。

**Parameters.Create.FileAttributes**并**Parameters.Create.EaLength**成员仅供使用的文件系统和文件系统筛选器驱动程序。 有关详细信息，请参阅[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)可安装文件系统 (IFS) 文档中的主题。

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

大多数设备和中间驱动程序将状态设置\_I/O 状态中的取得成功的 IRP 阻止并完成创建请求，但驱动程序可以选择使用其[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)若要保留该句柄的任何后续 I/O 请求的资源的回调函数。 例如，系统串行驱动程序将其调出代码映射并分配所需处理后续尝试打开的输入和输出设备的用户模式线程的 I/O 请求任何资源。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IO\_安全\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff550613)

[**ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)

 

 





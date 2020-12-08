---
title: IRP_MJ_QUERY_INFORMATION
description: 驱动程序可以选择处理 IRP_MJ_QUERY_INFORMATION 请求。
ms.date: 08/12/2017
keywords:
- IRP_MJ_QUERY_INFORMATION Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: e33200124377670eaefd239af8ad95228ab08230
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813047"
---
# <a name="irp_mj_query_information"></a>IRP\_MJ\_QUERY\_INFORMATION


驱动程序可以选择处理 **IRP \_ MJ \_ 查询 \_ 信息** 请求。

<a name="when-sent"></a>发送时间
---------

操作系统将发送 **IRP \_ MJ \_ 查询 \_ 信息** 请求，以获取有关文件或文件句柄的元数据。 例如，当驱动程序调用 [**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)时，操作系统将发送 **IRP \_ MJ \_ 查询 \_ 信息** 请求。

## <a name="input-parameters"></a>输入参数


**QueryFile. FileInformationClass** 成员是一个 **文件 \_ 信息 \_ 类** 常量，用于指定要提供的元数据的类型。 有关元数据类型的详细信息，请参阅 [**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)例程的 *FileInformationClass* 参数。

**QueryFile** 成员指定 **AssociatedIrp.SystemBuffer** 成员所指向的缓冲区的长度。

## <a name="output-parameters"></a>输出参数


**AssociatedIrp.SystemBuffer** 成员指向驱动程序提供所请求信息的缓冲区。 **QueryFile. FileInformationClass** 的值确定) 要返回的 **\_ *XXX* \_ 文件** 的元数据 (格式。 有关元数据格式的详细信息，请参阅 [**文件 \_ 信息 \_ 类**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class) 枚举。

<a name="operation"></a>操作
---------

无需驱动程序即可处理此请求，不需要驱动程序处理每个可能的 **参数值。 QueryFile. FileInformationClass**。 \_ \_ 对于任何不处理的值，驱动程序的调度例程应返回错误代码，如状态无效的设备 \_ 请求。

不可能出现 [**文件 \_ 信息 \_ 类**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class) 的所有可能值。

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

## <a name="see-also"></a>请参阅


[**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

 


---
title: IRP_MJ_SET_INFORMATION
description: 设备驱动程序可以选择处理 IRP_MJ_SET_INFORMATION 请求。
ms.date: 08/12/2017
keywords:
- IRP_MJ_SET_INFORMATION Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 88e15d88c06e64817e72c83864ac9008a2261cb8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837227"
---
# <a name="irp_mj_set_information"></a>IRP\_MJ\_SET\_INFORMATION


设备驱动程序可以选择处理 **IRP \_ MJ \_ 集 \_ 信息** 请求。

<a name="when-sent"></a>发送时间
---------

操作系统发送 **IRP \_ MJ \_ 集 \_ 信息** 请求，以设置关于文件或文件句柄的元数据。 例如，当驱动程序调用 [**ZwSetInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)时，操作系统将发送 **IRP \_ MJ \_ 集 \_ 信息** 请求。

## <a name="input-parameters"></a>输入参数


**SetFile. FileInformationClass** 成员是一个 **文件 \_ 信息 \_ 类** 常量，它指定要设置的元数据的类型。 有关元数据类型的详细信息，请参阅 [**ZwSetInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)的 *FileInformationClass* 参数。

**SetFile** 成员指定 **AssociatedIrp.SystemBuffer** 成员所指向的缓冲区的长度。

**AssociatedIrp.SystemBuffer** 指向包含新信息设置的缓冲区。 **SetFile. FileInformationClass** 的值确定) 要返回的 **\_ *XXX* \_ 文件** (的数据格式。 有关元数据格式的详细信息，请参阅 [**文件 \_ 信息 \_ 类**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class) 枚举。

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

无需驱动程序即可处理此请求，不需要驱动程序处理每个可能的 **参数值。 SetFile. FileInformationClass**。 \_ \_ 对于任何不处理的值，驱动程序的调度例程应返回错误代码，如状态无效的设备 \_ 请求。

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


[**ZwSetInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)

 


---
title: IRP_MJ_SET_INFORMATION
description: 设备驱动程序可以选择处理 IRP_MJ_SET_INFORMATION 请求。
ms.date: 08/12/2017
ms.assetid: 1bcca676-2926-4d0f-9c0f-c6ea56481153
keywords:
- IRP_MJ_SET_INFORMATION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: f3406e691b4e60bf43fd5bccdcf0f5f5b40e8269
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838597"
---
# <a name="irp_mj_set_information"></a>IRP\_MJ\_SET\_INFORMATION


设备驱动程序可以选择处理**IRP\_MJ\_集\_信息**请求。

<a name="when-sent"></a>发送时间
---------

操作系统将**IRP\_MJ 发送\_设置\_信息**请求，以设置关于文件或文件句柄的元数据。 例如，当驱动程序调用[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)时，操作系统将发送**IRP\_MJ\_集\_信息**请求。

## <a name="input-parameters"></a>输入参数


**SetFile. FileInformationClass**成员是一个 **\_信息\_类**常量的文件，用于指定要设置的元数据的类型。 有关元数据类型的详细信息，请参阅[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)的*FileInformationClass*参数。

**SetFile**成员指定**AssociatedIrp 的 SystemBuffer**成员指向的缓冲区的长度。

**AssociatedIrp. SystemBuffer**指向包含新信息设置的缓冲区。 **SetFile. FileInformationClass**的值确定要返回的数据的格式（ **\_*XXX*\_信息**结构的文件）。 有关元数据格式的详细信息，请参阅[**文件\_信息\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)枚举。

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

无需驱动程序即可处理此请求，不需要驱动程序处理每个可能的**参数值。 SetFile. FileInformationClass**。 驱动程序的调度例程应返回错误代码，例如状态\_无效\_设备\_请求它不处理的任何值。

不是所有可能的文件值[ **\_信息\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)可能发生。

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


[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)

 

 





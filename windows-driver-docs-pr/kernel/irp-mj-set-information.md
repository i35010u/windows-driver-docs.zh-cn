---
title: IRP_MJ_SET_INFORMATION
description: 设备驱动程序可以根据需要处理 IRP_MJ_SET_INFORMATION 请求。
ms.date: 08/12/2017
ms.assetid: 1bcca676-2926-4d0f-9c0f-c6ea56481153
keywords:
- IRP_MJ_SET_INFORMATION Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 5d9f09dae2974297c39c5b901eff114f38906e7d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368438"
---
# <a name="irpmjsetinformation"></a>IRP\_MJ\_SET\_INFORMATION


设备驱动程序可以根据需要处理**IRP\_MJ\_设置\_信息**请求。

<a name="when-sent"></a>发送时间
---------

操作系统发送**IRP\_MJ\_设置\_信息**设置有关的文件或文件句柄的元数据请求。 例如，当驱动程序调用[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)，操作系统发送**IRP\_MJ\_设置\_信息**请求。

## <a name="input-parameters"></a>输入参数


**Parameters.SetFile.FileInformationClass**成员是**文件\_信息\_类**常量，它指定要设置元数据的类型。 有关类型的元数据的详细信息，请参阅*FileInformationClass*的参数[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)。

**Parameters.SetFile.Length**成员指定缓冲区的长度， **AssociatedIrp.SystemBuffer**成员指向。

**AssociatedIrp.SystemBuffer**指向包含新的信息设置的缓冲区。 值**Parameters.SetFile.FileInformationClass**确定数据的格式 (**文件\_*XXX*\_信息**结构） 返回。 有关的元数据格式的详细信息，请参阅[**文件\_信息\_类**](https://msdn.microsoft.com/library/windows/hardware/ff728840)枚举。

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

驱动程序不需要处理此请求，并执行操作的驱动程序不需要处理的每个可能值**Parameters.SetFile.FileInformationClass**。 驱动程序的调度例程应返回类似于状态错误代码\_无效\_设备\_不处理任何值的请求。

并非所有的可能值[**文件\_信息\_类**](https://msdn.microsoft.com/library/windows/hardware/ff728840)可能发生。

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


[**ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)

 

 





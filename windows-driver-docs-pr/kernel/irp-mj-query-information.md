---
title: IRP_MJ_QUERY_INFORMATION
description: 驱动程序可以根据需要处理 IRP_MJ_QUERY_INFORMATION 请求。
ms.date: 08/12/2017
ms.assetid: 317f82b1-88d3-4618-9282-140eca2178b5
keywords:
- IRP_MJ_QUERY_INFORMATION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: a9f7260d59759bf5640425cef6724c34c2c30710
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565643"
---
# <a name="irpmjqueryinformation"></a>IRP\_MJ\_QUERY\_INFORMATION


驱动程序可以根据需要处理**IRP\_MJ\_查询\_信息**请求。

<a name="when-sent"></a>发送时间
---------

操作系统发送**IRP\_MJ\_查询\_信息**请求以获取有关文件或文件句柄的元数据。 例如，当驱动程序调用[ **ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052)，操作系统发送**IRP\_MJ\_查询\_信息**请求。

## <a name="input-parameters"></a>输入参数


**Parameters.QueryFile.FileInformationClass**成员是**文件\_信息\_类**常量，它指定要提供元数据的类型。 有关类型的元数据的详细信息，请参阅*FileInformationClass*的参数[ **ZwQueryInformationFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567052)例程。

**Parameters.QueryFile.Length**成员指定缓冲区的长度， **AssociatedIrp.SystemBuffer**成员指向。

## <a name="output-parameters"></a>输出参数


**AssociatedIrp.SystemBuffer**成员指向的缓冲区位置驱动程序提供所需的信息。 值**Parameters.QueryFile.FileInformationClass**确定元数据的格式 (**文件\_*XXX*\_信息**结构） 返回。 有关的元数据格式的详细信息，请参阅[**文件\_信息\_类**](https://msdn.microsoft.com/library/windows/hardware/ff728840)枚举。

<a name="operation"></a>操作
---------

驱动程序不需要处理此请求，并执行操作的驱动程序不需要处理的每个可能值**Parameters.QueryFile.FileInformationClass**。 驱动程序的调度例程应返回类似于状态错误代码\_无效\_设备\_不处理任何值的请求。

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


[**ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052)

 

 





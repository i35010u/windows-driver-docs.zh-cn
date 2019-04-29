---
title: IRP_MJ_POWER
description: 所有驱动程序必须准备为 DispatchPower 例程中 IRP_MJ_POWER 请求提供服务。
ms.date: 08/12/2017
ms.assetid: ca53ceef-2755-49d3-aab9-0d12a0e51e75
keywords:
- IRP_MJ_POWER Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 0355a600ffe5ebd9e27358c95106966727382f5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368471"
---
# <a name="irpmjpower"></a>IRP\_MJ\_POWER


所有驱动程序必须准备对服务**IRP\_MJ\_POWER**中的请求[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

<a name="when-sent"></a>发送时间
---------

电源管理器或驱动程序可以发送**IRP\_MJ\_POWER**请求在任何时间运行的操作系统。

## <a name="input-parameters"></a>输入参数


取决于处的值**MinorFunction**中当前的 I/O 堆栈 IRP 的位置。 每个**IRP\_MJ\_POWER**请求指定了次要函数代码用于标识请求的电源操作。

## <a name="output-parameters"></a>输出参数


取决于处的值**MinorFunction**中当前的 I/O 堆栈 IRP 的位置。

<a name="operation"></a>操作
---------

除了处理 Irp，进行控制的常用规则**IRP\_MJ\_POWER** Irp 具有以下特殊要求：接收电源的驱动程序 IRP 不得更改任何 I/O 堆栈中的位置 IRP，电源管理器或更高级别的驱动程序已设置的主版本号和次函数代码。 电源管理器依赖于这些函数代码，直到完成 IRP 保持不变。 此规则冲突的情况可能会导致难以调试的问题。 例如，操作系统可能会停止响应，或者"挂起"。

请参阅[电源管理次要 Irp](power-management-minor-irps.md)有关详细信息**IRP\_MJ\_POWER**请求。

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


[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 





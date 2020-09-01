---
title: IRP_MJ_POWER
description: 所有驱动程序都必须准备好在 DispatchPower 例程中处理 IRP_MJ_POWER 请求。
ms.date: 08/12/2017
ms.assetid: ca53ceef-2755-49d3-aab9-0d12a0e51e75
keywords:
- IRP_MJ_POWER 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 6f516a809ff48355ea52f01c29dc3a74f167dae5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188263"
---
# <a name="irp_mj_power"></a>IRP\_MJ\_POWER


所有驱动程序都必须准备好在[*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中为**IRP \_ MJ \_ POWER**请求服务。

<a name="when-sent"></a>发送时间
---------

在操作系统运行时，电源管理器或驱动程序可以发送 **IRP \_ MJ \_ 电源** 请求。

## <a name="input-parameters"></a>输入参数


依赖于 IRP 当前 i/o 堆栈位置中 **MinorFunction** 处的值。 每个 **IRP \_ MJ \_ POWER** request 指定标识所请求电源操作的次要函数代码。

## <a name="output-parameters"></a>输出参数


依赖于 IRP 当前 i/o 堆栈位置中 **MinorFunction** 处的值。

<a name="operation"></a>操作
---------

除了控制对 Irp 的处理的常规规则外， **IRP \_ MJ \_ 电源** irp 还具有以下特殊要求：接收 power IRP 的驱动程序不得更改 IRP 中任何 i/o 堆栈位置的主要和次要函数代码，这些位置已由 POWER manager 或高级驱动程序设置。 在完成 IRP 之前，power manager 依赖于这些函数代码保持不变。 违反此规则会导致难以调试的问题。 例如，操作系统可能会停止响应或 "挂起"。

有关**IRP \_ MJ \_ 电源**请求的详细信息，请参阅[电源管理次要 irp](power-management-minor-irps.md) 。

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


[*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 


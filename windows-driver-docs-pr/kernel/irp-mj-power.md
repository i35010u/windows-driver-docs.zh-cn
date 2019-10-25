---
title: IRP_MJ_POWER
description: 所有驱动程序必须准备好在 DispatchPower 例程中处理 IRP_MJ_POWER 请求。
ms.date: 08/12/2017
ms.assetid: ca53ceef-2755-49d3-aab9-0d12a0e51e75
keywords:
- IRP_MJ_POWER 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 7ebe72a1d26fdd9196f9f0cc6eac3b3784d2829b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828103"
---
# <a name="irp_mj_power"></a>IRP\_MJ\_POWER


所有驱动程序都必须做好准备，以便在[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中 **\_POWER requests\_MJ**进行 service IRP。

<a name="when-sent"></a>发送时间
---------

当操作系统每次运行时，电源管理器或驱动程序都可以将**IRP\_MJ 发送\_电源**请求。

## <a name="input-parameters"></a>输入参数


依赖于 IRP 当前 i/o 堆栈位置中**MinorFunction**处的值。 每个**IRP\_MJ\_POWER** request 指定用于标识请求的电源操作的次要函数代码。

## <a name="output-parameters"></a>输出参数


依赖于 IRP 当前 i/o 堆栈位置中**MinorFunction**处的值。

<a name="operation"></a>操作
---------

除了控制 Irp 处理的常用规则， **IRP\_MJ\_电源**irp 具有以下特殊要求：接收 POWER irp 的驱动程序不得更改中任何 i/o 堆栈位置的主要和次要函数代码由 power manager 或更高级别的驱动程序设置的 IRP。 在完成 IRP 之前，power manager 依赖于这些函数代码保持不变。 违反此规则会导致难以调试的问题。 例如，操作系统可能会停止响应或 "挂起"。

有关 IRP 的详细信息，请参阅[电源管理次要 irp](power-management-minor-irps.md) **\_POWER requests\_MJ** 。

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


[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 





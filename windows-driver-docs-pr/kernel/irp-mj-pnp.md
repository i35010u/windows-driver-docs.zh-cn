---
title: IRP_MJ_PNP
description: 所有驱动程序都必须准备好在 DispatchPnP 例程中处理 IRP_MJ_PNP 请求。
ms.date: 08/12/2017
keywords:
- IRP_MJ_PNP Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 926af81d72fcfe0a7a310a1b3b939882e29d62e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822320"
---
# <a name="irp_mj_pnp"></a>IRP\_MJ\_PNP


所有驱动程序必须准备好在 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中为 **IRP \_ MJ \_ PNP** 请求服务。

<a name="when-sent"></a>发送时间
---------

PnP 管理器在枚举、资源重新平衡以及系统上即插即用活动发生的任何其他时间发送 **IRP \_ MJ \_ PnP** 请求。 驱动程序还可以发送某些 **IRP \_ MJ \_ PNP** 请求，具体取决于次要函数代码。

## <a name="input-parameters"></a>输入参数


依赖于 IRP 当前 i/o 堆栈位置中 **MinorFunction** 处的值。 每个 **IRP \_ MJ \_ PNP** 请求指定一个用于标识所请求的 PNP 操作的次要函数代码。

## <a name="output-parameters"></a>输出参数


依赖于 IRP 当前 i/o 堆栈位置中 **MinorFunction** 处的值。

<a name="operation"></a>操作
---------

请参阅 [即插即用次 irp](plug-and-play-minor-irps.md) ，获取有关 **IRP \_ MJ \_ PNP** 请求的详细信息。

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


[*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 


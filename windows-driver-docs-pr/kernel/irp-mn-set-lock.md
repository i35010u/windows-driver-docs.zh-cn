---
title: IRP_MN_SET_LOCK
description: 总线驱动程序必须为其子设备处理此 IRP， (支持设备锁定的子 PDOs) 。 函数和筛选器驱动程序不处理此请求。
ms.date: 08/12/2017
ms.assetid: d4e09527-f817-4eb5-b0f5-7584de8888b1
keywords:
- IRP_MN_SET_LOCK 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 5083b4e24f9b029e7903fafa6edfeeb0a6c77563
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106938"
---
# <a name="irp_mn_set_lock"></a>IRP \_ MN \_ 设置 \_ 锁定


总线驱动程序必须为其子设备处理此 IRP， (支持设备锁定的子 PDOs) 。 函数和筛选器驱动程序不处理此请求。

## <a name="value"></a>“值”

0x12

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器会将此 IRP 发送到，以便将驱动程序 (s) 锁定设备，并阻止设备弹出或解锁设备。

PnP 管理器在 \_ 任意线程上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**SetLock**成员是一个布尔值，指定是否将 () 或解锁 (FALSE) 设备。

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/o 状态块


总线驱动程序将 **Irp- &gt; IoStatus** 设置为 " \_ 成功" 或相应的 "错误" 状态。

成功时，驱动程序将 **Irp- &gt; IoStatus** 设置为零。

如果总线驱动程序未处理此 IRP，它会将 **irp- &gt; IoStatus** 保持原样，并完成 irp。

函数和筛选器驱动程序不处理此 IRP。 此类驱动程序调用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) ，并将 IRP 向下传递到下一个驱动程序。 函数和筛选器驱动程序不会设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，不能修改 **irp- &gt; IoStatus**，也不能完成 Irp。

<a name="operation"></a>操作
---------

如果驱动程序为此 IRP 返回成功，则会确保设备在完成 IRP 之前已锁定或解锁。

请参阅 [即插即用](./introduction-to-plug-and-play.md) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

预留给系统使用。 驱动程序不得发送此 IRP。

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

 


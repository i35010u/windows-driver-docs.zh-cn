---
title: IRP_MN_QUERY_REMOVE_DEVICE
description: 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 95ec9ed8-014f-4d01-bed7-3aeb29cd9e73
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: d1e08382ac4baed50223f931954133902e294cdd
ms.sourcegitcommit: 68d0aec4c282c9c1e1ab54509c8f4575dd273d56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2020
ms.locfileid: "91221959"
---
# <a name="irp_mn_query_remove_device"></a>IRP \_ MN \_ 查询 \_ 删除 \_ 设备


所有 PnP 驱动程序都必须处理此 IRP。

## <a name="value"></a>值

0x01

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器发送此 IRP，以通知驱动程序要从计算机中删除设备，并查询是否可以在不中断计算机的情况下删除设备。 如果用户请求更新设备的驱动程序 () ，PnP 管理器还会发送此 IRP。

PnP 管理器在 \_ 系统线程的上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/o 状态块


驱动程序将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"，或设置为适当的错误状态，如状态 "未 \_ 成功"。

<a name="operation"></a>Operation
---------

此 IRP 首先由设备堆栈顶部的驱动程序处理，然后向下传递到堆栈中的每个较低的驱动程序。

为了响应此 IRP，驱动程序指示是否可以在不中断计算机的情况下删除设备。

有关处理此 IRP 的详细信息，请参阅 [处理 irp \_ MN \_ 查询 \_ 删除 \_ 设备请求](./handling-an-irp-mn-query-remove-device-request.md)。 有关支持设备删除的一般信息，请参阅 [删除设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device-in-a-function-driver)。

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

## <a name="see-also"></a>请参阅


[**IRP \_ MN \_ 取消 \_ 删除 \_ 设备**](irp-mn-cancel-remove-device.md)

[**IRP \_ MN \_ 设备 \_ 使用 \_ 通知**](irp-mn-device-usage-notification.md)

[**IRP \_ MN \_ 删除 \_ 设备**](irp-mn-remove-device.md)

 


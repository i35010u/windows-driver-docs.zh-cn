---
title: IRP_MN_QUERY_REMOVE_DEVICE
description: 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 95ec9ed8-014f-4d01-bed7-3aeb29cd9e73
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 60ee3539877e440b40533b3a97fe0510bbeedaaa
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922600"
---
# <a name="irp_mn_query_remove_device"></a>IRP\_MN\_查询\_删除\_设备


所有 PnP 驱动程序都必须处理此 IRP。

## <a name="value"></a>值

0x01

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器发送此 IRP，以通知驱动程序要从计算机中删除设备，并查询是否可以在不中断计算机的情况下删除设备。 如果用户请求更新设备的驱动程序，PnP 管理器还会发送此 IRP。

PnP 管理器在系统线程的上下文中\_以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


None

## <a name="output-parameters"></a>输出参数


None

## <a name="io-status-block"></a>I/o 状态块


驱动程序将**Irp-&gt;IOSTATUS**设置为状态\_"成功"，或设置为适当的错误状态\_，如状态 "未成功"。

<a name="operation"></a>操作
---------

此 IRP 首先由设备堆栈顶部的驱动程序处理，然后向下传递到堆栈中的每个较低的驱动程序。

为了响应此 IRP，驱动程序指示是否可以在不中断计算机的情况下删除设备。

有关处理此 IRP 的详细信息，请参阅[处理 irp\_MN\_查询\_删除\_设备请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-query-remove-device-request)。 有关支持设备删除的一般信息，请参阅[删除设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)。

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

## <a name="see-also"></a>另请参阅


[**IRP\_MN\_取消\_删除\_设备**](irp-mn-cancel-remove-device.md)

[**IRP\_MN\_设备\_使用\_通知**](irp-mn-device-usage-notification.md)

[**IRP\_MN\_删除\_设备**](irp-mn-remove-device.md)

 

 





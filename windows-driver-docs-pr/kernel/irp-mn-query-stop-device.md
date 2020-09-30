---
title: IRP_MN_QUERY_STOP_DEVICE
description: 了解 "IRP_MN_QUERY_STOP_DEVICE" 内核模式驱动程序体系结构。 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 22f58964-23a0-4307-a748-9c1620e30871
keywords:
- IRP_MN_QUERY_STOP_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: a7496870afc1aedd874065e695a71e14a7905939
ms.sourcegitcommit: 2aedb606f9f14e74687f0d3da60e14fc6ffffa7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91544406"
---
# <a name="irp_mn_query_stop_device"></a>IRP \_ MN \_ 查询 \_ 停止 \_ 设备


所有 PnP 驱动程序都必须处理此 IRP。

## <a name="value"></a>值

0x05

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器发送此 IRP 以查询是否可以停止设备以重新平衡资源。

在 Windows 98/Me 上，PnP 管理器还会在设备被禁用时发送此 IRP。

PnP 管理器在 \_ 系统线程的上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


None

## <a name="output-parameters"></a>输出参数


None

## <a name="io-status-block"></a>I/o 状态块


驱动程序将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功" 或相应的 "错误" 状态。 如果驱动程序无法停止设备，则驱动程序将 **Irp- &gt; IoStatus** 设置为状态 "未 \_ 成功"。

总线驱动程序可以将 **irp &gt; IoStatus** 设置为状态 \_ 资源 \_ 需求 \_ 更改为指示 Irp 成功，同时还要求 PNP 管理器在发送停止 Irp 之前再次查询设备的资源要求。

<a name="operation"></a>Operation
---------

此 IRP 首先由设备堆栈顶部的驱动程序处理，然后向下传递到堆栈中的每个较低的驱动程序。

为了响应此 IRP，驱动程序指示停止设备以便重新平衡资源是否安全。

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

## <a name="see-also"></a>请参阅


[**IRP \_ MN \_ 取消 \_ 停止 \_ 设备**](irp-mn-cancel-stop-device.md)

[**IRP \_ MN \_ 设备 \_ 使用 \_ 通知**](irp-mn-device-usage-notification.md)

[**IRP \_ MN \_ 启动 \_ 设备**](irp-mn-start-device.md)

[**IRP \_ MN \_ 停止 \_ 设备**](irp-mn-stop-device.md)

 

 





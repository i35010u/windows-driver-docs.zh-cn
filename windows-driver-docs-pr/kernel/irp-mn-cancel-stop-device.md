---
title: IRP_MN_CANCEL_STOP_DEVICE
description: 了解 "IRP_MN_CANCEL_STOP_DEVICE" 内核模式驱动程序体系结构。 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
keywords:
- IRP_MN_CANCEL_STOP_DEVICE Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 579d3de079e707d3cb8780838d839fe1778b4252
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823997"
---
# <a name="irp_mn_cancel_stop_device"></a>IRP \_ MN \_ 取消 \_ 停止 \_ 设备


所有 PnP 驱动程序都必须处理此 IRP。

## <a name="value"></a>“值”

0x06

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器将在 [**irp \_ MN \_ 查询 \_ 停止 \_ 设备**](irp-mn-query-stop-device.md)之后的某个时间发送此 IRP，通知设备的驱动程序，该设备将不会被禁用 (Windows 98/Me 仅) 或停止资源重新配置。

PnP 管理器在 \_ 系统线程的上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/o 状态块


对于此 IRP，驱动程序必须将 **irp &gt; IoStatus** 设置为状态 " \_ 成功"。 如果驱动程序未通过此 IRP，则设备处于不一致状态。

<a name="operation"></a>操作
---------

此 IRP 必须首先由设备的父总线驱动程序处理，然后由设备堆栈中的每个更高的驱动程序处理。

为了响应此 IRP，驱动程序将设备恢复到 "已启动" 状态。 当设备处于停止挂起状态时，驱动程序将启动任何已持有的 Irp。

如果设备在接收到此 IRP 时已处于活动状态，则函数或筛选器驱动程序只需将状态设置为 "成功"，并将 IRP 传递到下一个驱动程序。 父总线驱动程序完成 IRP。 对于这种取消-停止 IRP，函数或筛选器驱动程序不需要设置完成例程。

请参阅 [即插即用](./introduction-to-plug-and-play.md) ，了解有关处理 stop irp 的详细信息以及处理所有 [即插即用次要 irp](plug-and-play-minor-irps.md)的常规规则。

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


[**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](irp-mn-query-stop-device.md)

 

 





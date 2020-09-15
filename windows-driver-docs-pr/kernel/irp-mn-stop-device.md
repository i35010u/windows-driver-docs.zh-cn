---
title: IRP_MN_STOP_DEVICE
description: 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: a5c81db0-e753-4d91-97e4-c58ea05f5ce8
keywords:
- IRP_MN_STOP_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 663bf26022804e2bdd7d04cc93722a5886d4090d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104578"
---
# <a name="irp_mn_stop_device"></a>IRP \_ MN \_ 停止 \_ 设备


所有 PnP 驱动程序都必须处理此 IRP。

## <a name="value"></a>值

0x04

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

PnP 管理器发送此 IRP 来停止设备，以便它可以重新配置设备的硬件资源。

在 Windows 2000 和更高版本的系统上，PnP 管理器仅在以前的 [**irp \_ MN \_ 查询 \_ 停止 \_ 设备**](irp-mn-query-stop-device.md) 成功完成后发送此 irp。

在 Windows 98/Me 上，PnP 管理器还会在设备被禁用时，以及当设备堆栈未通过 **IRP \_ MN \_ 启动 \_ 设备** 请求时发送此 IRP。 如果启动失败，PnP 管理器会发送此 IRP，而不会出现前面的 [**irp \_ MN \_ 查询 \_ 停止 \_ 设备**](irp-mn-query-stop-device.md) 请求。

PnP 管理器在 \_ 系统线程的上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/o 状态块


驱动程序必须将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

<a name="operation"></a>操作
---------

此 IRP 首先由设备堆栈顶部的驱动程序处理，然后向下传递到堆栈中的每个较低的驱动程序。

为了响应此 IRP，Windows 2000 和更高版本的驱动程序会停止设备，并释放设备使用的任何硬件资源，如 i/o 端口和中断。

在 Windows 2000 和更高版本上，停止 IRP 仅用于释放设备的硬件资源，以便可以重新配置这些资源。 重新配置资源后，将重新启动设备。 停止 IRP 不是删除 IRP 的前提。 有关 PnP Irp 发送到设备的顺序的详细信息，请参阅 [即插即用](./introduction-to-plug-and-play.md) 。

在 Windows 98/Me 上，还可以在启动失败之后和设备处于禁用状态时使用 "停止 IRP"。 在这些操作系统上运行的 WDM 驱动程序应停止设备，使任何传入 i/o 失败，并禁用和取消注册任何用户模式接口。

驱动程序不能使此 IRP 失败。 如果驱动程序无法释放设备的硬件资源，则必须使前面的查询停止 IRP 失败。

有关处理停止 Irp 的详细信息，请参阅 [停止设备](./stopping-a-device.md) 。

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

[**IRP \_ MN \_ 启动 \_ 设备**](irp-mn-start-device.md)

[**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)

[**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

 


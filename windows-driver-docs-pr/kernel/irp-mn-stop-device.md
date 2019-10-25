---
title: IRP_MN_STOP_DEVICE
description: 所有 PnP 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: a5c81db0-e753-4d91-97e4-c58ea05f5ce8
keywords:
- IRP_MN_STOP_DEVICE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 03bc3143324d86265bac7855dc3a7727d2569b7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827950"
---
# <a name="irp_mn_stop_device"></a>IRP\_MN\_停止\_设备


所有 PnP 驱动程序都必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)发送时间
---------

PnP 管理器发送此 IRP 来停止设备，以便它可以重新配置设备的硬件资源。

在 Windows 2000 和更高版本的系统上，仅当之前的[**irp\_MN\_QUERY\_停止\_设备**](irp-mn-query-stop-device.md)成功完成时，PnP 管理器才会发送此 IRP。

在 Windows 98/Me 上，PnP 管理器还会在以下情况下发送此 IRP：当设备处于禁用状态时，如果设备堆栈未通过**IRP\_MN\_开始\_设备**请求。 如果启动失败，PnP 管理器将在没有前面的[**irp\_MN\_QUERY\_停止\_设备**](irp-mn-query-stop-device.md)请求的情况下发送此 irp。

PnP 管理器以 IRQL 被动\_级别在系统线程的上下文中发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序必须将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS。

<a name="operation"></a>操作
---------

此 IRP 首先由设备堆栈顶部的驱动程序处理，然后向下传递到堆栈中的每个较低的驱动程序。

为了响应此 IRP，Windows 2000 和更高版本的驱动程序会停止设备，并释放设备使用的任何硬件资源，如 i/o 端口和中断。

在 Windows 2000 和更高版本上，停止 IRP 仅用于释放设备的硬件资源，以便可以重新配置这些资源。 重新配置资源后，将重新启动设备。 停止 IRP 不是删除 IRP 的前提。 有关 PnP Irp 发送到设备的顺序的详细信息，请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

在 Windows 98/Me 上，还可以在启动失败之后和设备处于禁用状态时使用 "停止 IRP"。 在这些操作系统上运行的 WDM 驱动程序应停止设备，使任何传入 i/o 失败，并禁用和取消注册任何用户模式接口。

驱动程序不能使此 IRP 失败。 如果驱动程序无法释放设备的硬件资源，则必须使前面的查询停止 IRP 失败。

有关处理停止 Irp 的详细信息，请参阅[停止设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/stopping-a-device)。

**正在发送此 IRP**

保留供系统使用。 驱动程序不得发送此 IRP。

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


[**IRP\_MN\_QUERY\_停止\_设备**](irp-mn-query-stop-device.md)

[**IRP\_MN\_启动\_设备**](irp-mn-start-device.md)

[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

 

 





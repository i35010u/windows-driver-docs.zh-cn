---
title: 驱动程序启动、停止和设备控制
description: 驱动程序启动、停止和设备控制
keywords:
- 小型重定向程序 WDK，开始
- 小型重定向程序 WDK，停止
- 小型重定向程序 WDK，设备控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93799313052b4e99d7bc5ce39a334586a2c8878c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823219"
---
# <a name="driver-start-stop-and-device-control"></a>驱动程序启动、停止和设备控制


驱动程序注册在网络小型重定向程序驱动程序的 **DriverEntry** 例程中处理。 当网络小型重定向程序首次开始 (在其 **DriverEntry** 例程) 中时，驱动程序必须调用 RDBSS [**RxRegisterMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr) 例程，以向 RDBSS 注册网络小型重定向程序。 网络小型重定向器传入了 MINIRDR \_ 调度结构，该结构包含配置数据和一 () 调度表，其中包含一个用于网络小型重定向程序驱动程序实现的例程的调度表。

[**MRxStart**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)和 [**MRxStop**](./mrxstop.md)例程必须由网络微重定向程序驱动程序实现，以允许启动和停止驱动程序。

用于启动或停止网络小型重定向器的序列非常复杂。 此顺序通常由网络微型重定向驱动程序提供的用户模式应用程序或服务启动，用于控制用于管理和管理的驱动程序。 网络小型重定向程序可以使用配置为在操作系统启动时自动启动的服务。 此服务可以请求在操作系统启动时启动网络小型重定向程序。

调用 [**RxStartMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr)例程时， [**MRxStart**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)由 RDBSS 调用。 **RxStartMinirdr** 例程通常作为来自用户模式应用程序或服务的 FSCTL 或 IOCTL 请求的结果被调用，以启动网络小型重定向程序。 成功调用 [**RxRegisterMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)后，不能从网络小型重定向程序的 **DriverEntry** 例程对 **RxStartMinirdr** 进行调用，因为某些启动处理要求完成驱动程序初始化。 接收到 **RxStartMinirdr** 调用后，RDBSS 将通过调用网络小型重定向器的 **MRxStart** 例程来完成启动过程。 如果对 **MRxStart** 的调用返回 success，则 RDBSS 会将 RDBSS 中的小型重定向器的内部状态设置为 "RDBSS \_ 已启动"。

调用 [**RxStopMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)例程时， [**MRxStop**](./mrxstop.md)由 RDBSS 调用。 通常将 RDBSS **RxStopMinirdr** 例程作为来自用户模式应用程序或服务的 FSCTL 或 IOCTL 请求，以停止网络微型重定向程序。 也可以通过网络小型重定向程序或操作系统的关闭过程的一部分来执行此调用。 接收到 **RxStopMinirdr** 调用后，RDBSS 将通过调用网络小型重定向器的 **MRxStop** 例程来完成此过程。

[**MRxDevFcbXXXControlFile**](./mrxdevfcbxxxcontrolfile.md)例程用于接收来自用户模式应用程序或服务的请求，通过在设备 FCB 上发出 IOCTL 或 FSCTL 调用来控制网络小型重定向程序。

此外，还提供了两个用于处理驱动程序对象上的 IOCTL 和 FSCTL 操作的低 i/o 例程： [**MRxLowIOSubmit \[ LOWIO \_ Op \_ FSCTL \]**](./mrxlowiosubmit-lowio-op-fsctl-.md)和 [**MRxLowIOSubmit \[ LOWIO \_ op \_ IOCTL \]**](./mrxlowiosubmit-lowio-op-ioctl-.md)。

网络小型重定向程序还可以使用这些低 i/o 例程从用户模式应用程序或服务提供网络微型重定向程序的控制和管理。

下表列出了可由网络小型重定向程序实现的、用于启动、停止和设备控制操作的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile" data-raw-source="[&lt;strong&gt;MRxDevFcbXXXControlFile&lt;/strong&gt;](./mrxdevfcbxxxcontrolfile.md)"><strong>MRxDevFcbXXXControlFile</strong></a></td>
<td align="left"><p>RDBSS 调用此例程将设备 FCB 控制请求传递到网络小型重定向程序。 RDBSS 发出此调用以响应在设备 FCB 上接收 IRP_MJ_DEVICE_CONTROL、IRP_MJ_FILE_SYSTEM_CONTROL 或 IRP_MJ_INTERNAL_DEVICE_CONTROL。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx" data-raw-source="[&lt;strong&gt;MRxStart&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)"><strong>MRxStart</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来启动网络小型重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/mrxstop" data-raw-source="[&lt;strong&gt;MRxStop&lt;/strong&gt;](./mrxstop.md)"><strong>MRxStop</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来停止网络微型重定向程序。</p></td>
</tr>
</tbody>
</table>

 


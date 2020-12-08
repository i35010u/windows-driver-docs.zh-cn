---
title: 驱动程序注册和启动/停止控件
description: 驱动程序注册和启动/停止控件
keywords:
- RDBSS WDK 文件系统，启动/停止控制
- 重定向的驱动器缓冲子系统 WDK 文件系统、启动/停止控制
- 启动/停止控件 WDK RDBSS
- RDBSS WDK 文件系统，驱动程序注册
- 重定向驱动器缓冲子系统 WDK 文件系统，驱动程序注册
- 驱动程序注册 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 952a27b7f0806af6c374c2770f6951bfd26fd7ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823215"
---
# <a name="driver-registration-and-startstop-control"></a>驱动程序注册和启动/停止控件


## <span id="ddk_driver_registration_and_start_stop_control_if"></span><span id="DDK_DRIVER_REGISTRATION_AND_START_STOP_CONTROL_IF"></span>


当操作系统启动时，Windows 会根据注册表中的设置加载 RDBSS 和任何网络微型重定向程序驱动程序。 对于使用 rdbsslib 进行静态链接的单一网络小型重定向程序驱动程序，驱动程序必须从其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用 [**RxDriverEntry**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry)例程，以初始化与网络驱动程序链接的 rdbsslib 库的副本。 在这种情况下，在调用和使用任何其他 RDBSS 例程之前，必须先调用 **RxDriverEntry** 例程。 对于非单一网络小型重定向程序驱动程序 (Microsoft SMB 重定向程序) ，在加载 rdbss.sys 设备驱动程序时，会在其自己的 **DriverEntry** 例程中进行初始化。

当驱动程序由内核加载并在卸载驱动程序时使用 RDBSS 取消注册时，网络小型重定向器将注册到 RDBSS。 网络小型重定向程序通知 RDBSS，它已通过调用 [**RxRegisterMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)（从 RDBSS 导出的注册例程）已加载。 作为此注册过程的一部分，网络小型重定向器会将参数传递给 **RxRegisterMinirdr** ，这是一个指向大型结构 MINIRDR 调度的指针 \_ 。 此结构包含网络小型重定向器的配置信息，以及指向由网络小型重定向程序内核驱动程序实现的回调例程的发送表。 RDBSS 通过此回调例程列表进行网络小型重定向器驱动程序的调用。

[**RxRegisterMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)例程将网络微型重定向程序驱动程序的所有驱动程序调度例程设置为指向顶级 RDBSS 调度例程 [**RxFsdDispatch**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch)。 网络小型重定向程序可通过以下方式重写此行为：保存其自己的入口点，并在调用 **RxRegisterMinirdr** 后重写驱动程序调度，并使用其自己的入口点重写此 **行为。**

网络微重定向程序驱动程序在收到对其 [**MRxStart**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx) 例程的调用（在 MINIRDR 调度结构中传递的回调例程之一）之前，不会实际启动操作 \_ 。 如果网络小型重定向程序驱动程序希望接收操作的回调例程（除非网络小型重定向程序保留其自己的驱动程序调度入口点），则必须使用 **MrxStart** 回调例程。 否则，RDBSS 只允许将以下 i/o 请求数据包传递到驱动程序，直到 **MrxStart** 成功返回：

-   IRP 的设备创建请求和设备操作，其中 IRPSP 的 &gt; 长度为零， &gt; RelatedFileObject 为 **NULL**。

对于任何其他 IRP 请求，RDBSS 调度例程 [**RxFsdDispatch**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch) 会返回状态 " \_ 重定向程序未启动" 状态 \_ \_ 。

RDBSS 调度例程还将无法处理以下 i/o 请求数据包：

-   IRP \_ MJ \_ CREATE \_ MAILSLOT

-   IRP \_ MJ \_ 创建 \_ 命名 \_ 管道

调用 [**RxStartMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr)例程时，由 RDBSS 调用由网络小型重定向程序实现的 [**MrxStart**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)回调例程。 RDBSS **RxStartMinirdr** 例程通常作为文件系统控制代码 (FSCTL) 或 i/o 控制代码， (IOCTL) 请求从用户模式应用程序或服务启动网络小型重定向程序。 成功调用 [**RxRegisterMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)后，不能从网络小型重定向程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程对 **RxStartMinirdr** 进行调用，因为某些启动处理要求完成驱动程序初始化。 接收到 **RxStartMinirdr** 调用后，RDBSS 将通过调用网络小型重定向器的 **MrxStart** 例程来完成启动过程。 如果对 **MrxStart** 的调用返回 success，则 RDBSS 会将 RDBSS 中的小型重定向器的内部状态设置为 "RDBSS \_ 已启动"。

RDBSS 导出例程 [**RxSetDomainForMailslotBroadcast**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast)，为 mailslot 广播设置域。 如果网络小型重定向程序支持 mailslots，则在注册过程中将使用此例程。

RDBSS 导出的便利例程 [**\_ \_ RxFillAndInstallFastIoDispatch**](/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)可用于将所有 IRP \_ MJ \_ XXX 驱动程序例程指针复制到可比较的快速 i/o 调度向量，但此例程仅适用于非单片驱动程序。

RDBSS 还会导出例程，通知 RDBSS 网络微型重定向程序正在启动或停止。 如果网络小型重定向器包括可启动和停止重定向程序的用户模式管理服务或实用程序，则使用这些调用。 此用户模式服务或应用程序可将自定义的 FSCTL 或 IOCTL 请求发送到网络小型重定向程序驱动程序，以指示它应启动或停止。 重定向程序可调用 RDBSS [**RxStartMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr) 或 [**RxStopMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr) 例程，通知 RDBSS 启动或停止此网络微型重定向程序。

下表列出了 RDBSS 驱动程序注册和启动/停止控制例程。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry" data-raw-source="[&lt;strong&gt;RxDriverEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry)"><strong>RxDriverEntry</strong></a></p></td>
<td align="left"><p>此例程由单一网络小型重定向程序驱动程序从其 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)"><strong>DriverEntry</strong></a> 例程调用，用于初始化 RDBSS。</p>
<p>对于非单片驱动程序，此初始化例程等效于 rbss.sys 设备驱动程序的 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)"><strong>DriverEntry</strong></a> 例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr" data-raw-source="[&lt;strong&gt;RxRegisterMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)"><strong>RxRegisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程由网络微重定向程序驱动程序调用，用于向 RDBSS 注册驱动程序，这会将注册信息添加到内部注册表。 RDBSS 还为网络小型重定向程序构建设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast" data-raw-source="[&lt;strong&gt;RxSetDomainForMailslotBroadcast&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast)"><strong>RxSetDomainForMailslotBroadcast</strong></a></p></td>
<td align="left"><p>如果驱动程序支持 mailslots，则网络微型重定向程序驱动程序将调用此例程来设置用于 mailslot 广播的域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr" data-raw-source="[&lt;strong&gt;RxStartMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr)"><strong>RxStartMinirdr</strong></a></p></td>
<td align="left"><p>此例程启动一个网络微型重定向程序，调用它来注册自身。 如果驱动程序指示支持 UNC 名称，则 RDBSS 还会将网络微型重定向程序驱动程序注册为包含 MUP 的 UNC 提供程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr" data-raw-source="[&lt;strong&gt;RxStopMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)"><strong>RxStopMinirdr</strong></a></p></td>
<td align="left"><p>此例程停止网络微型重定向程序驱动程序。 已停止的驱动程序将不再接收 IOCTL 或 FSCTL 请求以外的新命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr)"><strong>RxpUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程由网络微型重定向程序驱动程序调用，用来向 RDBSS 反注册驱动程序，并从内部 RDBSS 注册表中删除注册信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr)"><strong>RxUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程是 rxstruc 中定义的内联函数，由网络微型重定向程序驱动程序调用，用于向 RDBSS 取消注册驱动程序并从内部 RDBSS 注册表中删除注册信息。 <a href="/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr)"><strong>RxUnregisterMinirdr</strong></a>内联函数在内部调用<a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr)"><strong>RxpUnregisterMinirdr</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a></p></td>
<td align="left"><p>此例程使用正常调度 i/o 向量完全相同的 i/o 调度向量，并将其安装到与传递的设备对象关联的驱动程序对象中。</p></td>
</tr>
</tbody>
</table>

 

以下宏在 mrx 头文件中定义，该文件调用这些例程之一。 通常使用此宏，而不是直接调用 [**\_ \_ RxFillAndInstallFastIoDispatch**](/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxFillAndInstallFastIoDispatch</strong> (<em>__devobj</em>， <em>__fastiodisp</em>) </p></td>
<td align="left"><p>此宏调用 <a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a>来填写快速 i/o 调度向量，使其与正常调度 i/o 向量相同，并将其安装到与传递的设备对象关联的驱动程序对象中。</p></td>
</tr>
</tbody>
</table>

 


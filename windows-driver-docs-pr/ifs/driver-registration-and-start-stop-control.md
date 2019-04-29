---
title: 驱动程序注册和启动/停止控件
description: 驱动程序注册和启动/停止控件
ms.assetid: 66f44703-1277-49fe-a481-c8712172db0f
keywords:
- RDBSS WDK 文件系统中，启动/停止控件
- 重定向驱动器缓冲子系统 WDK 文件系统中，启动/停止控件
- 启动/停止控件 WDK RDBSS
- RDBSS WDK 文件系统驱动程序注册
- 重定向驱动器缓冲子系统 WDK 的文件系统，驱动程序注册
- 驱动程序注册 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd265f9d8848d53821cb240a432657f655b02ffb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359493"
---
# <a name="driver-registration-and-startstop-control"></a>驱动程序注册和启动/停止控件


## <span id="ddk_driver_registration_and_start_stop_control_if"></span><span id="DDK_DRIVER_REGISTRATION_AND_START_STOP_CONTROL_IF"></span>


当启动操作系统时，Windows 将加载 RDBSS 和基于注册表中设置的任何网络微型重定向程序驱动程序。 对于整体化网络微型重定向程序驱动程序，可以与 rdbsslib.lib 以静态方式链接时，该驱动程序必须调用[ **RxDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554404)例程从其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，以初始化 RDBSSLIB 库的副本链接网络驱动程序。 在这种情况下， **RxDriverEntry**必须之前已调用和使用任何其他 RDBSS 例程调用例程。 对于非整体化网络微型重定向程序驱动程序 （Microsoft SMB 重定向程序），rdbss.sys 设备驱动程序初始化在自己**DriverEntry**例程时加载。

该驱动程序由内核加载和卸载该驱动程序时使用 RDBSS 注销时，向 RDBSS 注册网络微型重定向。 网络微型重定向将通知它已通过调用已加载 RDBSS [ **RxRegisterMinirdr**](https://msdn.microsoft.com/library/windows/hardware/ff554693)，从 RDBSS 导出注册例程。 作为此注册过程的一部分，网络微型重定向将传递的参数**RxRegisterMinirdr** ，它是指向一个大型的结构，MINIRDR\_调度。 此结构包含网络微型重定向和调度表指向由网络微型重定向程序内核驱动程序实现的回调例程的指针的配置信息。 RDBSS 调用回调例程的此列表的网络微型重定向程序驱动程序。

[ **RxRegisterMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554693)例程设置驱动程序的所有网络微型重定向程序驱动程序，以指向顶级 RDBSS 调度例程的调度例程[ **RxFsdDispatch**](https://msdn.microsoft.com/library/windows/hardware/ff554468)。 网络微型重定向可以替代此行为通过将保存其自己的入口点的调用后重写其自己的入口点与驱动程序调度**RxRegisterMinirdr**返回或设置特殊参数时调用**RxRegisterMinirdr**。

网络微型重定向程序驱动程序实际上不会启动操作直到接收到调用其[ **MRxStart** ](https://msdn.microsoft.com/library/windows/hardware/ff550829)例程，其中一个回调例程中传递 MINIRDR\_调度结构。 **MrxStart**网络微型重定向程序驱动程序必须实现的回调例程，如果其希望接收操作的回调例程，除非网络微型重定向将保留其自己的驱动程序调度入口点。 否则，RDBSS 将仅允许以下 I/O 请求数据包通过向驱动程序直到**MrxStart**成功返回：

-   设备会创建请求 IRP 和设备操作其中的文件对象的&gt;FileName.Length IRPSP 上的是零，文件对象的&gt;RelatedFileObject 是**NULL**。

对于任何其他 IRP 请求，RDBSS 调度例程[ **RxFsdDispatch** ](https://msdn.microsoft.com/library/windows/hardware/ff554468)将返回状态的状态\_重定向程序\_不\_已启动。

RDBSS 调度例程也将失败，以下的 I/O 请求数据包的任何请求：

-   IRP\_MJ\_CREATE\_MAILSLOT

-   IRP\_MJ\_CREATE\_NAMED\_PIPE

[ **MrxStart** ](https://msdn.microsoft.com/library/windows/hardware/ff550829) RDBSS 调用回调例程实现通过网络微型重定向时[ **RxStartMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554736)调用例程。 RDBSS **RxStartMinirdr**例程通常称为文件系统控制代码 (FSCTL) 的结果或从启动网络微型重定向的用户模式应用程序或服务请求的 I/O 控制代码 (IOCTL)。 在调用**RxStartMinirdr**不能从进行[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)网络微型-重定向程序在成功调用后的日常[ **RxRegisterMinirdr**](https://msdn.microsoft.com/library/windows/hardware/ff554693)因为一些开始处理需要完成驱动程序初始化。 一次**RxStartMinirdr**接收到调用、 RDBSS 完成启动过程通过调用**MrxStart**网络微型重定向的例程。 如果在调用**MrxStart**返回成功，RDBSS 设置最小-重定向程序的内部状态中到 RDBSS RDBSS\_已启动。

RDBSS 导出例程[ **RxSetDomainForMailslotBroadcast**](https://msdn.microsoft.com/library/windows/hardware/ff554718)，将设置为邮件槽广播域。 如果网络微型重定向支持 mailslot，在注册期间使用此例程。

方便起见例程[  **\_ \_RxFillAndInstallFastIoDispatch**](https://msdn.microsoft.com/library/windows/hardware/ff557374)、 导出由 RDBSS 可用于复制所有 IRP\_MJ\_XXX 驱动程序用于处理可比较的快速 i/o 的 I/O 请求处理例程的指针调度向量，但此例程仅适用于非整体化驱动程序。

RDBSS 还将导出例程，从而通知 RDBSS，启动或停止网络微型重定向。 如果网络微型重定向包括用户模式下管理服务，则使用这些调用或启动和停止重定向程序的实用程序应用程序。 此用户模式服务或应用程序可以向网络微型重定向程序驱动程序，以指示它应启动或停止发送自定义 FSCTL 或 IOCTL 请求。 重定向程序可以调用 RDBSS [ **RxStartMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554736)或[ **RxStopMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554743)例程，从而通知 RDBSS 启动或停止此网络最小-重定向程序。

下表列出了 RDBSS 驱动程序注册和启动/停止控制例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554404" data-raw-source="[&lt;strong&gt;RxDriverEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554404)"><strong>RxDriverEntry</strong></a></p></td>
<td align="left"><p>此例程称为由单一式网络微型重定向程序驱动程序从其<a href="https://msdn.microsoft.com/library/windows/hardware/ff544113" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544113)"> <strong>DriverEntry</strong> </a>例程，以初始化 RDBSS。</p>
<p>对于非整体化驱动程序，此初始化例程等同于<a href="https://msdn.microsoft.com/library/windows/hardware/ff544113" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544113)"> <strong>DriverEntry</strong> </a>例程 rbss.sys 设备驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554693" data-raw-source="[&lt;strong&gt;RxRegisterMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554693)"><strong>RxRegisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程称为网络微型重定向程序驱动程序，该驱动程序注册到 RDBSS，将注册信息添加到内部注册表。 RDBSS 还生成网络微型重定向的设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554718" data-raw-source="[&lt;strong&gt;RxSetDomainForMailslotBroadcast&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554718)"><strong>RxSetDomainForMailslotBroadcast</strong></a></p></td>
<td align="left"><p>此例程称为网络微型重定向程序驱动程序，如果 mailslot 支持的驱动程序，则设置为邮件槽广播，使用的域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554736" data-raw-source="[&lt;strong&gt;RxStartMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554736)"><strong>RxStartMinirdr</strong></a></p></td>
<td align="left"><p>此例程会启动网络微型重定向的调用以注册其自身。 RDBSS 还将将网络微型重定向程序驱动程序注册为 MUP UNC 提供程序，如驱动程序，表示 UNC 名称的支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554743" data-raw-source="[&lt;strong&gt;RxStopMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554743)"><strong>RxStopMinirdr</strong></a></p></td>
<td align="left"><p>此例程将停止网络微型重定向程序驱动程序。 除了 IOCTL 或 FSCTL 请求，已停止的驱动程序将不再接收新的命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554662" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554662)"><strong>RxpUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程称为网络的最小重定向程序驱动程序取消注册与 RDBSS 驱动程序并从内部 RDBSS registration 表中删除注册信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554744" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554744)"><strong>RxUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程是内联函数中称为网络的最小重定向程序驱动程序取消注册与 RDBSS 驱动程序并从内部 RDBSS registration 表中删除注册信息的 rxstruc.h 定义。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff554744" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554744)"> <strong>RxUnregisterMinirdr</strong> </a>内联函数在内部调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff554662" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554662)"> <strong>RxpUnregisterMinirdr</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557374" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557374)"><strong>__RxFillAndInstallFastIoDispatch</strong></a></p></td>
<td align="left"><p>此例程填写快速 I/O 调度向量为与正常调度 I/O 向量相同，并将其安装到与传递的设备对象关联的驱动程序对象。</p></td>
</tr>
</tbody>
</table>

 

下面的宏调用每个例程 mrx.h 标头文件中定义。 而不是调用通常使用此宏[  **\_ \_RxFillAndInstallFastIoDispatch** ](https://msdn.microsoft.com/library/windows/hardware/ff557374)直接例程。

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
<td align="left"><p><strong>RxFillAndInstallFastIoDispatch</strong>(<em>__devobj</em>, <em>__fastiodisp</em>)</p></td>
<td align="left"><p>此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff557374" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557374)"> <strong>__RxFillAndInstallFastIoDispatch</strong></a>填写快速 I/O 调度向量相同正常调度 I/O 向量，其驱动程序对象与关联的安装传递的设备对象。</p></td>
</tr>
</tbody>
</table>

 

 

 





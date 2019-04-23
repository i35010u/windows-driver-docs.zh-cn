---
title: WDM IRP 和 WDF 事件回调函数
description: WDM IRP 和 WDF 事件回调函数
ms.assetid: 9B9A01FD-AA15-4C30-B19D-2F6451014EAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 553532e917a0132afde5ef726696dc0d88af0076
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902494"
---
# <a name="wdm-irps-and-wdf-event-callback-functions"></a>WDM IRP 和 WDF 事件回调函数


内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 支持 Windows Irp 的子集。 下表列出了主要的 WDM IRP 类型和相应的 framework 事件回调函数。 除非另行指定，回调将适用于 KMDF 和 UMDF。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主要 IRP 代码</th>
<th align="left">WDF 事件回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550718" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550718)"><strong>IRP_MJ_CLEANUP</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541700" data-raw-source="[&lt;em&gt;EvtFileCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541700)"><em>EvtFileCleanup</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550720" data-raw-source="[&lt;strong&gt;IRP_MJ_CLOSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550720)"><strong>IRP_MJ_CLOSE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541702" data-raw-source="[&lt;em&gt;EvtFileClose&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541702)"><em>EvtFileClose</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550729" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550729)"><strong>IRP_MJ_CREATE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540868" data-raw-source="[&lt;em&gt;EvtDeviceFileCreate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540868)"><em>EvtDeviceFileCreate</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="even">
<td align="left">IRP_MJ_CREATE_MAILSLOT</td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left">IRP_MJ_DEVICE_CHANGE</td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550744" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550744)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541758" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541758)"><em>EvtIoDeviceControl</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff548658" data-raw-source="[&lt;strong&gt;IRP_MJ_DIRECTORY_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548658)"><strong>IRP_MJ_DIRECTORY_CONTROL</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550751" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550751)"><strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550760" data-raw-source="[&lt;strong&gt;IRP_MJ_FLUSH_BUFFERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550760)"><strong>IRP_MJ_FLUSH_BUFFERS</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550766" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550766)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541768" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541768)"><em>EvtIoInternalDeviceControl</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549251" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549251)"><strong>IRP_MJ_LOCK_CONTROL</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550772" data-raw-source="[&lt;strong&gt;IRP_MJ_PNP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550772)"><strong>IRP_MJ_PNP</strong></a></td>
<td align="left">很多;请参阅<a href="#kmdf-callbacks-for-irp_mj_pnp" data-raw-source="[KMDF Callbacks for IRP_MJ_PNP](#kmdf-callbacks-for-irp_mj_pnp)">IRP_MJ_PNP KMDF 回调</a>。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550784" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550784)"><strong>IRP_MJ_POWER</strong></a></td>
<td align="left">很多;请参阅<a href="#kmdf-callbacks-for-irp_mj_power" data-raw-source="[KMDF Callbacks for IRP_MJ_POWER](#kmdf-callbacks-for-irp_mj_power)">IRP_MJ_POWER KMDF 回调</a>。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549279" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_EA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549279)"><strong>IRP_MJ_QUERY_EA</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550788" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550788)"><strong>IRP_MJ_QUERY_INFORMATION</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549293" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549293)"><strong>IRP_MJ_QUERY_QUOTA</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549298" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_SECURITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549298)"><strong>IRP_MJ_QUERY_SECURITY</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549318" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549318)"><strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550794" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550794)"><strong>IRP_MJ_READ</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"><em>EvtIoRead</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549346" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_EA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549346)"><strong>IRP_MJ_SET_EA</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550799" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550799)"><strong>IRP_MJ_SET_INFORMATION</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549401" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_QUOTA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549401)"><strong>IRP_MJ_SET_QUOTA</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549407" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_SECURITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549407)"><strong>IRP_MJ_SET_SECURITY</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549415" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549415)"><strong>IRP_MJ_SET_VOLUME_INFORMATION</strong></a></td>
<td align="left">不能直接支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550807" data-raw-source="[&lt;strong&gt;IRP_MJ_SHUTDOWN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550807)"><strong>IRP_MJ_SHUTDOWN</strong></a></td>
<td align="left"><p>对于控制的设备对象，实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540911" data-raw-source="[&lt;em&gt;EvtDeviceShutdownNotification (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540911)"> <em>EvtDeviceShutdownNotification (仅适用于 KMDF)</em></a></p>
<p>对于所有插设备对象：不支持;实现<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (仅适用于 KMDF)</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550813" data-raw-source="[&lt;strong&gt;IRP_MJ_SYSTEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550813)"><strong>IRP_MJ_SYSTEM_CONTROL</strong></a></td>
<td align="left">创建 WDFWMIPROVIDER 和 WDFWMIINSTANCE 对象和实施<strong>EvtWmiXxx (仅适用于 KMDF)</strong>回调。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550819" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550819)"><strong>IRP_MJ_WRITE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541813" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541813)"><em>EvtIoWrite</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
</tbody>
</table>

 

## <a name="kmdf-callbacks-for-irpmjpnp"></a>KMDF IRP 的回调\_MJ\_PNP


下表列出了，按顺序执行，对应的次要 IRP 代码 KMDF 回调[ **IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)。 箭头表示传输时堆栈上下 WDM FDO 是否处理 IRP。

**请注意**  中 KMDF 驱动程序、 插和电源管理是集成的操作，该驱动程序不会接收的各次[ **IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)或[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)请求。 相反，框架将调用的回调在打开电源，并且相应设置能耗更低，为一组核心，并调用其他回调之前和之后根据单个即插即用的每个请求需要设置此核心。 有关显示的启动和关闭序列的全面关系图，请参阅[移植 PnP 和电源管理功能](porting-pnp-and-power-management-functionality.md)。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IRP_MJ_PNP 细微的代码</th>
<th align="left">KMDF 回调</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff550823" data-raw-source="[&lt;strong&gt;IRP_MN_CANCEL_REMOVE_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550823)"><strong>IRP_MN_CANCEL_REMOVE_DEVICE</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff550826" data-raw-source="[&lt;strong&gt;IRP_MN_CANCEL_STOP_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550826)"><strong>IRP_MN_CANCEL_STOP_DEVICE</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="odd">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff550841" data-raw-source="[&lt;strong&gt;IRP_MN_DEVICE_USAGE_NOTIFICATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550841)"><strong>IRP_MN_DEVICE_USAGE_NOTIFICATION</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540915" data-raw-source="[&lt;em&gt;EvtDeviceUsageNotification&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540915)"><em>EvtDeviceUsageNotification</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff550853" data-raw-source="[&lt;strong&gt;IRP_MN_EJECT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550853)"><strong>IRP_MN_EJECT</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540863" data-raw-source="[&lt;em&gt;EvtDeviceEject (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540863)"><em>EvtDeviceEject (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff550874" data-raw-source="[&lt;strong&gt;IRP_MN_FILTER_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550874)"><strong>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540872" data-raw-source="[&lt;em&gt;EvtDeviceFilterRemoveResourceRequirements (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540872)"><em>EvtDeviceFilterRemoveResourceRequirements (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff550874" data-raw-source="[&lt;strong&gt;IRP_MN_FILTER_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550874)"><strong>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540870" data-raw-source="[&lt;em&gt;EvtDeviceFilterAddResourceRequirements (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540870)"><em>EvtDeviceFilterAddResourceRequirements (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551654" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_BUS_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551654)"><strong>IRP_MN_QUERY_BUS_INFORMATION</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法，以便该框架可以响应对此查询在其自己而无需通知驱动程序在初始化过程中设置设备属性。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551664" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551664)"><strong>IRP_MN_QUERY_CAPABILITIES</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法，以便该框架可以响应对此查询在其自己而无需通知驱动程序在初始化过程中设置设备属性。</td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551670" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_DEVICE_RELATIONS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551670)"><strong>IRP_MN_QUERY_DEVICE_RELATIONS</strong> </a> （总线、 删除和弹出关系）</td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540886" data-raw-source="[&lt;em&gt;EvtDeviceRelationsQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540886)"><em>EvtDeviceRelationsQuery</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551674" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_DEVICE_TEXT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551674)"><strong>IRP_MN_QUERY_DEVICE_TEXT</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法，以便该框架可以响应对此查询在其自己而无需通知驱动程序在初始化过程中设置设备属性。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551679" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551679)"><strong>IRP_MN_QUERY_ID</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法，以便该框架可以响应对此查询在其自己而无需通知驱动程序在初始化过程中设置设备属性。</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551687" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551687)"><strong>IRP_MN_QUERY_INTERFACE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540882" data-raw-source="[&lt;em&gt;EvtDeviceProcessQueryInterfaceRequest (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540882)"><em>EvtDeviceProcessQueryInterfaceRequest (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551698" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_PNP_DEVICE_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551698)"><strong>IRP_MN_QUERY_PNP_DEVICE_STATE</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法，以便该框架可以响应对此查询在其自己而无需通知驱动程序在初始化过程中设置设备属性。</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551705" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_REMOVE_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551705)"><strong>IRP_MN_QUERY_REMOVE_DEVICE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540883" data-raw-source="[&lt;em&gt;EvtDeviceQueryRemove&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540883)"><em>EvtDeviceQueryRemove</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551715" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551715)"><strong>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540894" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540894)"><em>EvtDeviceResourceRequirementsQuery (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551710" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551710)"><strong>IRP_MN_QUERY_RESOURCES</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540895" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540895)"><em>EvtDeviceResourcesQuery (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551725" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_STOP_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551725)"><strong>IRP_MN_QUERY_STOP_DEVICE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540885" data-raw-source="[&lt;em&gt;EvtDeviceQueryStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540885)"><em>EvtDeviceQueryStop</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551727" data-raw-source="[&lt;strong&gt;IRP_MN_READ_CONFIG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551727)"><strong>IRP_MN_READ_CONFIG</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法，以便该框架可以响应对此查询在其自己而无需通知驱动程序在初始化过程中设置设备属性。</td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551738" data-raw-source="[&lt;strong&gt;IRP_MN_REMOVE_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551738)"><strong>IRP_MN_REMOVE_DEVICE</strong></a></td>
<td align="left"><p>之后<a href="https://msdn.microsoft.com/library/windows/hardware/ff551705" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_REMOVE_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551705)"> <strong>IRP_MN_QUERY_REMOVE_DEVICE</strong></a>:</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionSuspend</strong>标志) <a href="https://msdn.microsoft.com/library/windows/hardware/ff541677" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541677)"> <em>EvtDmaEnablerSelfManagedIoStop (仅适用于 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540927" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540927)"><em>EvtDmaEnablerDisable (仅适用于 KMDF)</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541655" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541655)"> <em>(仅适用于 KMDF) EvtDmaEnablerFlush</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540856" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540856)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541714" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541714)"><em>EvtInterruptDisable</em></a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"> <em>EvtDeviceD0Exit</em> </a> (<strong>WdfPowerDeviceD3Final</strong>状态) <a href="https://msdn.microsoft.com/library/windows/hardware/ff540890" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540890)"> <em>EvtDeviceReleaseHardware</em></a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"> <em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionPurge</strong>标志) 的电源管理队列<a href="https://msdn.microsoft.com/library/windows/hardware/ff540901" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540901)"> <em>EvtDeviceSelfManagedIoFlush</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionPurge</strong>标志) 的电源管理队列<a href="https://msdn.microsoft.com/library/windows/hardware/ff540898" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540898)"> <em>EvtDeviceSelfManagedIoCleanup</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540840" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540840)"><em>EvtCleanupCallback</em> </a>为 WDFDEVICE <a href="https://msdn.microsoft.com/library/windows/hardware/ff540841" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540841)"> <em>EvtDestroyCallback</em> </a>为 WDFDEVICE
<p>之后<a href="https://msdn.microsoft.com/library/windows/hardware/ff551760" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551760)"> <strong>IRP_MN_SURPRISE_REMOVAL</strong></a>:</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionPurge</strong>标志) 的电源管理队列<a href="https://msdn.microsoft.com/library/windows/hardware/ff540898" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540898)"> <em>EvtDeviceSelfManagedIoCleanup</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540840" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540840)"><em>EvtCleanupCallback</em> </a>为 WDFDEVICE <a href="https://msdn.microsoft.com/library/windows/hardware/ff540841" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540841)"> <em>EvtDestroyCallback</em> </a>为 WDFDEVICE</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551742" data-raw-source="[&lt;strong&gt;IRP_MN_SET_LOCK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551742)"><strong>IRP_MN_SET_LOCK</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540909" data-raw-source="[&lt;em&gt;EvtDeviceSetLock (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540909)"><em>EvtDeviceSetLock (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff551749" data-raw-source="[&lt;strong&gt;IRP_MN_START_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551749)"><strong>IRP_MN_START_DEVICE</strong></a></td>
<td align="left"><p>之后枚举：</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540892" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540892)"><em>(仅适用于 KMDF) EvtDeviceRemoveAddedResources</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"><em>EvtDevicePrepareHardware</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"><em>EvtDeviceD0Entry</em> </a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541730" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541730)"> <em>EvtInterruptEnable</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540853" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540853)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540932" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540932)"> <em>(仅适用于 KMDF) EvtDmaEnablerFill</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540929" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540929)"><em>EvtDmaEnablerEnable (仅适用于 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541663" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541663)"><em>EvtDmaEnablerSelfManagedIoStart (仅 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540902" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoInit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540902)"><em>EvtDeviceSelfManagedIoInit</em></a>
<p>之后<a href="https://msdn.microsoft.com/library/windows/hardware/ff551755" data-raw-source="[&lt;strong&gt;IRP_MN_STOP_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551755)"> <strong>IRP_MN_STOP_DEVICE</strong></a>:</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540892" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540892)"><em>(仅适用于 KMDF) EvtDeviceRemoveAddedResources</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"><em>EvtDevicePrepareHardware</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"><em>EvtDeviceD0Entry</em> </a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541730" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541730)"> <em>EvtInterruptEnable</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540853" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540853)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540932" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540932)"> <em>(仅适用于 KMDF) EvtDmaEnablerFill</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540929" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540929)"><em>EvtDmaEnablerEnable (仅适用于 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541663" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541663)"><em>EvtDmaEnablerSelfManagedIoStart (仅 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541779" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541779)"><em>EvtIoResume</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540905" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540905)"><em>EvtDeviceSelfManagedIoRestart</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551755" data-raw-source="[&lt;strong&gt;IRP_MN_STOP_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551755)"><strong>IRP_MN_STOP_DEVICE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionSuspend</strong>标志) <a href="https://msdn.microsoft.com/library/windows/hardware/ff541677" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541677)"> <em>EvtDmaEnablerSelfManagedIoStop (仅适用于 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540927" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540927)"><em>EvtDmaEnablerDisable (仅适用于 KMDF)</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541655" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541655)"> <em>(仅适用于 KMDF) EvtDmaEnablerFlush</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540856" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540856)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541714" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541714)"><em>EvtInterruptDisable</em></a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"> <em>EvtDeviceD0Exit</em> </a> (<strong>WdfPowerDeviceD3Final</strong>状态) <a href="https://msdn.microsoft.com/library/windows/hardware/ff540890" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540890)"> <em>EvtDeviceReleaseHardware</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551760" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551760)"><strong>IRP_MN_SURPRISE_REMOVAL</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540913" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540913)"><em>EvtDeviceSurpriseRemoval</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionSuspend</strong>标志) <a href="https://msdn.microsoft.com/library/windows/hardware/ff541677" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541677)"> <em>EvtDmaEnablerSelfManagedIoStop (仅适用于 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540927" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540927)"><em>EvtDmaEnablerDisable (仅适用于 KMDF)</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541655" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541655)"> <em>EvtDmaEnablerFlush (仅适用于 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540856" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540856)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em> </a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541714" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541714)"> <em>EvtInterruptDisable</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"><em>EvtDeviceD0Exit</em> </a> (<strong>WdfPowerDeviceD3Final</strong>状态) <a href="https://msdn.microsoft.com/library/windows/hardware/ff540890" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540890)"> <em>EvtDeviceReleaseHardware</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionPurge</strong>标志) 的电源管理队列<a href="https://msdn.microsoft.com/library/windows/hardware/ff540901" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540901)"> <em>EvtDeviceSelfManagedIoFlush</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551769" data-raw-source="[&lt;strong&gt;IRP_MN_WRITE_CONFIG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551769)"><strong>IRP_MN_WRITE_CONFIG</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法，以便该框架可以响应对此查询在其自己而无需通知驱动程序在初始化过程中设置设备属性。</td>
</tr>
</tbody>
</table>

 

## <a name="kmdf-callbacks-for-irpmjpower"></a>KMDF IRP 的回调\_MJ\_电源


下表列出了，按顺序执行，对应的次要 IRP 代码 KMDF 回调[ **IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784)。 箭头表示传输时堆栈上下 WDM FDO 是否处理 IRP。

**请注意**  注意：在 KMDF 驱动程序，插和电源管理是集成的操作，该驱动程序不会收到单独的次要[ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)或[**IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)请求。 相反，框架将调用的回调在打开电源，并且相应设置能耗更低，为一组核心，并调用其他回调之前和之后根据单个即插即用的每个请求需要设置此核心。 有关显示的启动和关闭序列的全面关系图，请参阅[移植 PnP 和电源管理功能](porting-pnp-and-power-management-functionality.md)。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IRP_MJ_POWER 细微的代码</th>
<th align="left">Framework 回调</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551744" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551744)"><strong>IRP_MN_SET_POWER</strong> </a> D1、 D2，或 D3 （关闭）</td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionSuspend</strong>标志) <a href="https://msdn.microsoft.com/library/windows/hardware/ff540843" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromS0&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540843)"> <em>EvtDeviceArmWakeFromS0</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff540844" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540844)"> <em>EvtDeviceArmWakeFromSx</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541677" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541677)"><em>EvtDmaEnablerSelfManagedIoStop (KMDF仅限）</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540927" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540927)"><em>EvtDmaEnablerDisable (仅适用于 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541655" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541655)"><em>EvtDmaEnablerFlush (仅适用于 KMDF)</em> </a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540856" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540856)"> <em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541714" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541714)"><em>EvtInterruptDisable</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"> <em>EvtDeviceD0Exit</em></a></td>
</tr>
<tr class="even">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff551744" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551744)"><strong>IRP_MN_SET_POWER</strong></a> for D0 (power up)</td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"><em>EvtDeviceD0Entry</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541730" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541730)"><em>EvtInterruptEnable</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540853" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540853)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540932" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540932)"> <em>EvtDmaEnablerFill (仅适用于 KMDF)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540929" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540929)"><em>EvtDmaEnablerEnable (仅适用于 KMDF)</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541663" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541663)"> <em>(仅适用于 KMDF) EvtDmaEnablerSelfManagedIoStart</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541779" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541779)"><em>EvtIoResume</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540905" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540905)"><em>EvtDeviceSelfManagedIoRestart</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551744" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551744)"><strong>IRP_MN_SET_POWER</strong></a> for Sx</td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff551744" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551744)"><strong>IRP_MN_SET_POWER</strong></a> for Sx</td>
<td align="left">无</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551644" data-raw-source="[&lt;strong&gt;IRP_MN_POWER_SEQUENCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551644)"><strong>IRP_MN_POWER_SEQUENCE</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551766" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551766)"><strong>IRP_MN_WAIT_WAKE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540866" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540866)"><em>EvtDeviceEnableWakeAtBus (仅适用于 KMDF)</em></a></td>
</tr>
<tr class="odd">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff551766" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551766)"><strong>IRP_MN_WAIT_WAKE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540858" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540858)"><em>EvtDeviceDisableWakeAtBus (仅适用于 KMDF)</em></a></td>
</tr>
</tbody>
</table>

 

 

 






---
title: WDM IRP 和 WDF 事件回调函数
description: WDM IRP 和 WDF 事件回调函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4126afd6505e8501a54b70b358fcc319754b59a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833943"
---
# <a name="wdm-irps-and-wdf-event-callback-functions"></a>WDM IRP 和 WDF 事件回调函数


Kernel-Mode Driver Framework (KMDF) 和 User-Mode Driver Framework (UMDF) 支持 Windows Irp 的一个子集。 下表列出了主要的 WDM IRP 类型和相应的框架事件回调函数。 除非另外指定，否则回调同时适用于 KMDF 和 UMDF。

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
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-cleanup" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](../kernel/irp-mj-cleanup.md)"><strong>IRP_MJ_CLEANUP</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup" data-raw-source="[&lt;em&gt;EvtFileCleanup&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)"><em>EvtFileCleanup</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-close" data-raw-source="[&lt;strong&gt;IRP_MJ_CLOSE&lt;/strong&gt;](../kernel/irp-mj-close.md)"><strong>IRP_MJ_CLOSE</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close" data-raw-source="[&lt;em&gt;EvtFileClose&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)"><em>EvtFileClose</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-create" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](../kernel/irp-mj-create.md)"><strong>IRP_MJ_CREATE</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create" data-raw-source="[&lt;em&gt;EvtDeviceFileCreate&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)"><em>EvtDeviceFileCreate</em></a>或<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="even">
<td align="left">IRP_MJ_CREATE_MAILSLOT</td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="odd">
<td align="left">IRP_MJ_DEVICE_CHANGE</td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](../kernel/irp-mj-device-control.md)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a>或<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-directory-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DIRECTORY_CONTROL&lt;/strong&gt;](../ifs/irp-mj-directory-control.md)"><strong>IRP_MJ_DIRECTORY_CONTROL</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-file-system-control" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](../kernel/irp-mj-file-system-control.md)"><strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-flush-buffers" data-raw-source="[&lt;strong&gt;IRP_MJ_FLUSH_BUFFERS&lt;/strong&gt;](../kernel/irp-mj-flush-buffers.md)"><strong>IRP_MJ_FLUSH_BUFFERS</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](../kernel/irp-mj-internal-device-control.md)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a>或<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-lock-control" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](../ifs/irp-mj-lock-control.md)"><strong>IRP_MJ_LOCK_CONTROL</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-pnp" data-raw-source="[&lt;strong&gt;IRP_MJ_PNP&lt;/strong&gt;](../kernel/irp-mj-pnp.md)"><strong>IRP_MJ_PNP</strong></a></td>
<td align="left">多年有关 IRP_MJ_PNP，请参阅 <a href="#kmdf-callbacks-for-irp_mj_pnp" data-raw-source="[KMDF Callbacks for IRP_MJ_PNP](#kmdf-callbacks-for-irp_mj_pnp)">KMDF 回调</a>。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](../kernel/irp-mj-power.md)"><strong>IRP_MJ_POWER</strong></a></td>
<td align="left">多年有关 IRP_MJ_POWER，请参阅 <a href="#kmdf-callbacks-for-irp_mj_power" data-raw-source="[KMDF Callbacks for IRP_MJ_POWER](#kmdf-callbacks-for-irp_mj_power)">KMDF 回调</a>。</td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-query-ea" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_EA&lt;/strong&gt;](../ifs/irp-mj-query-ea.md)"><strong>IRP_MJ_QUERY_EA</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-query-information" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_INFORMATION&lt;/strong&gt;](../kernel/irp-mj-query-information.md)"><strong>IRP_MJ_QUERY_INFORMATION</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-query-quota" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](../ifs/irp-mj-query-quota.md)"><strong>IRP_MJ_QUERY_QUOTA</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-query-security" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_SECURITY&lt;/strong&gt;](../ifs/irp-mj-query-security.md)"><strong>IRP_MJ_QUERY_SECURITY</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-query-volume-information" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_VOLUME_INFORMATION&lt;/strong&gt;](../ifs/irp-mj-query-volume-information.md)"><strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](../kernel/irp-mj-read.md)"><strong>IRP_MJ_READ</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>或<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-set-ea" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_EA&lt;/strong&gt;](../ifs/irp-mj-set-ea.md)"><strong>IRP_MJ_SET_EA</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-set-information" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_INFORMATION&lt;/strong&gt;](../kernel/irp-mj-set-information.md)"><strong>IRP_MJ_SET_INFORMATION</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-set-quota" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_QUOTA&lt;/strong&gt;](../ifs/irp-mj-set-quota.md)"><strong>IRP_MJ_SET_QUOTA</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-set-security" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_SECURITY&lt;/strong&gt;](../ifs/irp-mj-set-security.md)"><strong>IRP_MJ_SET_SECURITY</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/irp-mj-set-volume-information" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_VOLUME_INFORMATION&lt;/strong&gt;](../ifs/irp-mj-set-volume-information.md)"><strong>IRP_MJ_SET_VOLUME_INFORMATION</strong></a></td>
<td align="left">无直接支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅实现 EVTDEVICEWDMIRPPREPROCESS (KMDF) </em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-shutdown" data-raw-source="[&lt;strong&gt;IRP_MJ_SHUTDOWN&lt;/strong&gt;](../kernel/irp-mj-shutdown.md)"><strong>IRP_MJ_SHUTDOWN</strong></a></td>
<td align="left"><p>对于控制设备对象， <a href="/windows-hardware/drivers/ddi/wdfcontrol/nc-wdfcontrol-evt_wdf_device_shutdown_notification" data-raw-source="[&lt;em&gt;EvtDeviceShutdownNotification (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfcontrol/nc-wdfcontrol-evt_wdf_device_shutdown_notification)"><em>仅实现 EVTDEVICESHUTDOWNNOTIFICATION (KMDF) </em></a></p>
<p>对于所有即插即用设备对象：不支持; <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>仅) 实现 EvtDeviceWdmIrpPreprocess (</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-system-control" data-raw-source="[&lt;strong&gt;IRP_MJ_SYSTEM_CONTROL&lt;/strong&gt;](../kernel/irp-mj-system-control.md)"><strong>IRP_MJ_SYSTEM_CONTROL</strong></a></td>
<td align="left">创建 WDFWMIPROVIDER 和 WDFWMIINSTANCE 对象，并 <strong> (仅) </strong> 回调来实现 EvtWmiXxx。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](../kernel/irp-mj-write.md)"><strong>IRP_MJ_WRITE</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a>或<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
</tbody>
</table>

 

## <a name="kmdf-callbacks-for-irp_mj_pnp"></a>IRP \_ MJ PNP 的 KMDF \_ 回调


下表按执行顺序列出了对应于 [**IRP \_ MJ \_ PNP**](../kernel/irp-mj-pnp.md)的次要 IRP 代码的 KMDF 回调。 箭头指示 WDM FDO 在传播到堆栈时是否处理 IRP。

**注意**   在 KMDF 驱动程序中，即插即用和电源管理是集成的操作，驱动程序不会收到单个次要 [**IRP \_ mj \_ PNP**](../kernel/irp-mj-pnp.md) 或 [**IRP \_ mj \_ power**](../kernel/irp-mj-power.md) 请求。 相反，框架在开机时调用一组核心回调，并在关闭时调用相应的设置，并在此核心集之前和之后调用其他每个即插即用请求的回调。 有关显示通电和关机顺序的综合关系图，请参阅 [移植 PnP 和电源管理功能](porting-pnp-and-power-management-functionality.md)。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IRP_MJ_PNP 次要代码</th>
<th align="left">KMDF 回调</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device" data-raw-source="[&lt;strong&gt;IRP_MN_CANCEL_REMOVE_DEVICE&lt;/strong&gt;](../kernel/irp-mn-cancel-remove-device.md)"><strong>IRP_MN_CANCEL_REMOVE_DEVICE</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device" data-raw-source="[&lt;strong&gt;IRP_MN_CANCEL_STOP_DEVICE&lt;/strong&gt;](../kernel/irp-mn-cancel-stop-device.md)"><strong>IRP_MN_CANCEL_STOP_DEVICE</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="odd">
<td align="left">↑<a href="/windows-hardware/drivers/kernel/irp-mn-device-usage-notification" data-raw-source="[&lt;strong&gt;IRP_MN_DEVICE_USAGE_NOTIFICATION&lt;/strong&gt;](../kernel/irp-mn-device-usage-notification.md)"><strong>IRP_MN_DEVICE_USAGE_NOTIFICATION</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification" data-raw-source="[&lt;em&gt;EvtDeviceUsageNotification&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification)"><em>EvtDeviceUsageNotification</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-eject" data-raw-source="[&lt;strong&gt;IRP_MN_EJECT&lt;/strong&gt;](../kernel/irp-mn-eject.md)"><strong>IRP_MN_EJECT</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject" data-raw-source="[&lt;em&gt;EvtDeviceEject (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)"><em>EvtDeviceEject (KMDF 仅) </em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements" data-raw-source="[&lt;strong&gt;IRP_MN_FILTER_RESOURCE_REQUIREMENTS&lt;/strong&gt;](../kernel/irp-mn-filter-resource-requirements.md)"><strong>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements" data-raw-source="[&lt;em&gt;EvtDeviceFilterRemoveResourceRequirements (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)"><em>EvtDeviceFilterRemoveResourceRequirements (KMDF 仅) </em></a></td>
</tr>
<tr class="even">
<td align="left">↑<a href="/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements" data-raw-source="[&lt;strong&gt;IRP_MN_FILTER_RESOURCE_REQUIREMENTS&lt;/strong&gt;](../kernel/irp-mn-filter-resource-requirements.md)"><strong>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements" data-raw-source="[&lt;em&gt;EvtDeviceFilterAddResourceRequirements (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)"><em>EvtDeviceFilterAddResourceRequirements (KMDF 仅) </em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mn-query-bus-information" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_BUS_INFORMATION&lt;/strong&gt;](../kernel/irp-mn-query-bus-information.md)"><strong>IRP_MN_QUERY_BUS_INFORMATION</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用 <strong>WdfDeviceInitXxx</strong> 方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mn-query-capabilities" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_CAPABILITIES&lt;/strong&gt;](../kernel/irp-mn-query-capabilities.md)"><strong>IRP_MN_QUERY_CAPABILITIES</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用 <strong>WdfDeviceInitXxx</strong> 方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="odd">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-query-device-relations" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_DEVICE_RELATIONS&lt;/strong&gt;](../kernel/irp-mn-query-device-relations.md)"><strong>IRP_MN_QUERY_DEVICE_RELATIONS</strong></a> (总线、删除和弹出关系) </td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_relations_query" data-raw-source="[&lt;em&gt;EvtDeviceRelationsQuery&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_relations_query)"><em>EvtDeviceRelationsQuery</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mn-query-device-text" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_DEVICE_TEXT&lt;/strong&gt;](../kernel/irp-mn-query-device-text.md)"><strong>IRP_MN_QUERY_DEVICE_TEXT</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用 <strong>WdfDeviceInitXxx</strong> 方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mn-query-id" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ID&lt;/strong&gt;](../kernel/irp-mn-query-id.md)"><strong>IRP_MN_QUERY_ID</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用 <strong>WdfDeviceInitXxx</strong> 方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="even">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-query-interface" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_INTERFACE&lt;/strong&gt;](../kernel/irp-mn-query-interface.md)"><strong>IRP_MN_QUERY_INTERFACE</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request" data-raw-source="[&lt;em&gt;EvtDeviceProcessQueryInterfaceRequest (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)"><em>EvtDeviceProcessQueryInterfaceRequest (KMDF 仅) </em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_PNP_DEVICE_STATE&lt;/strong&gt;](../kernel/irp-mn-query-pnp-device-state.md)"><strong>IRP_MN_QUERY_PNP_DEVICE_STATE</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用 <strong>WdfDeviceInitXxx</strong> 方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="even">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-query-remove-device" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_REMOVE_DEVICE&lt;/strong&gt;](../kernel/irp-mn-query-remove-device.md)"><strong>IRP_MN_QUERY_REMOVE_DEVICE</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove" data-raw-source="[&lt;em&gt;EvtDeviceQueryRemove&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)"><em>EvtDeviceQueryRemove</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCE_REQUIREMENTS&lt;/strong&gt;](../kernel/irp-mn-query-resource-requirements.md)"><strong>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)"><em>EvtDeviceResourceRequirementsQuery (KMDF 仅) </em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-query-resources" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCES&lt;/strong&gt;](../kernel/irp-mn-query-resources.md)"><strong>IRP_MN_QUERY_RESOURCES</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)"><em>EvtDeviceResourcesQuery (KMDF 仅) </em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-query-stop-device" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_STOP_DEVICE&lt;/strong&gt;](../kernel/irp-mn-query-stop-device.md)"><strong>IRP_MN_QUERY_STOP_DEVICE</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop" data-raw-source="[&lt;em&gt;EvtDeviceQueryStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)"><em>EvtDeviceQueryStop</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mn-read-config" data-raw-source="[&lt;strong&gt;IRP_MN_READ_CONFIG&lt;/strong&gt;](../kernel/irp-mn-read-config.md)"><strong>IRP_MN_READ_CONFIG</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用 <strong>WdfDeviceInitXxx</strong> 方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="odd">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-remove-device" data-raw-source="[&lt;strong&gt;IRP_MN_REMOVE_DEVICE&lt;/strong&gt;](../kernel/irp-mn-remove-device.md)"><strong>IRP_MN_REMOVE_DEVICE</strong></a></td>
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-query-remove-device" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_REMOVE_DEVICE&lt;/strong&gt;](../kernel/irp-mn-query-remove-device.md)"><strong>IRP_MN_QUERY_REMOVE_DEVICE</strong></a>后：</p>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> (<strong>WDFREQUESTSTOPACTIONSUSPEND</strong>标志) <a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)"><em>EVTDMAENABLERSELFMANAGEDIOSTOP (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)"><em>EvtDmaEnablerDisable (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)"><em>EvtDmaEnablerFlush (KMDF) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)"><em>EvtInterruptDisable</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a> (<strong>WdfPowerDeviceD3Final</strong> state) <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)"><em>EvtDeviceReleaseHardware</em></a>
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> <strong> (WdfRequestStopActionPurge EvtDeviceSelfManagedIoFlush EvtIoStop WdfRequestStopActionPurge</strong> <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)"><em>EvtDeviceSelfManagedIoCleanup EvtCleanupCallback</em></a> <a href="/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)"><em>WDFDEVICE</em></a> <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)"><em>EvtDestroyCallback WDFDEVICE</em></a>
<a href="/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)"><em>EvtCleanupCallback</em></a> 
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> <strong>WdfRequestStopActionPurge</strong>
<p><a href="/windows-hardware/drivers/kernel/irp-mn-surprise-removal" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](../kernel/irp-mn-surprise-removal.md)"><strong>IRP_MN_SURPRISE_REMOVAL</strong></a>后：</p>
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> (<strong>WdfRequestStopActionPurge</strong>) 标志，适用于非电源管理的队列<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)"><em>EvtDeviceSelfManagedIoCleanup</em></a>
<a href="/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)"><em>EvtCleanupCallback</em></a> for <a href="/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)"><em>WDFDEVICE EvtDestroyCallback for WDFDEVICE</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-set-lock" data-raw-source="[&lt;strong&gt;IRP_MN_SET_LOCK&lt;/strong&gt;](../kernel/irp-mn-set-lock.md)"><strong>IRP_MN_SET_LOCK</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock" data-raw-source="[&lt;em&gt;EvtDeviceSetLock (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)"><em>EvtDeviceSetLock (KMDF 仅) </em></a></td>
</tr>
<tr class="odd">
<td align="left">↑<a href="/windows-hardware/drivers/kernel/irp-mn-start-device" data-raw-source="[&lt;strong&gt;IRP_MN_START_DEVICE&lt;/strong&gt;](../kernel/irp-mn-start-device.md)"><strong>IRP_MN_START_DEVICE</strong></a></td>
<td align="left"><p>枚举后：</p>
<a href="/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)"><em>EvtDeviceRemoveAddedResources (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EVTDEVICED0ENTRY</em></a>
<a href="/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)"><em>EvtInterruptEnable</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)"><em>EvtDmaEnablerFill (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)"><em>EvtDmaEnablerEnable (</em></a>KMDF 仅) 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)"><em>EvtDmaEnablerSelfManagedIoStart (KMDF </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoInit&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)"><em>) </em></a>
<p><a href="/windows-hardware/drivers/kernel/irp-mn-stop-device" data-raw-source="[&lt;strong&gt;IRP_MN_STOP_DEVICE&lt;/strong&gt;](../kernel/irp-mn-stop-device.md)"><strong>IRP_MN_STOP_DEVICE</strong></a>后：</p>
<a href="/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)"><em>EvtDeviceRemoveAddedResources (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EVTDEVICED0ENTRY</em></a>
<a href="/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)"><em>EvtInterruptEnable</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)"><em>EvtDmaEnablerFill (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)"><em>EvtDmaEnablerEnable (</em></a>KMDF 仅) 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)"><em>EvtDmaEnablerSelfManagedIoStart (KMDF </em></a>) 
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>EvtIoResume EvtDeviceSelfManagedIoRestart</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)"><em>EvtDeviceSelfManagedIoRestart</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-stop-device" data-raw-source="[&lt;strong&gt;IRP_MN_STOP_DEVICE&lt;/strong&gt;](../kernel/irp-mn-stop-device.md)"><strong>IRP_MN_STOP_DEVICE</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> (<strong>WDFREQUESTSTOPACTIONSUSPEND</strong>标志) <a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)"><em>EVTDMAENABLERSELFMANAGEDIOSTOP (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)"><em>EvtDmaEnablerDisable (KMDF</em></a>仅) 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)"><em>EvtDmaEnablerFlush (KMDF </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)"><em>) EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)"><em>EvtInterruptDisable</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a> (<strong>WdfPowerDeviceD3Final</strong> state) <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)"><em>EvtDeviceReleaseHardware</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-surprise-removal" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](../kernel/irp-mn-surprise-removal.md)"><strong>IRP_MN_SURPRISE_REMOVAL</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"><em>EvtDeviceSurpriseRemoval</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> (<strong>WdfRequestStopActionSuspend</strong>标志) <a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)"><em>EvtDmaEnablerSelfManagedIoStop (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)"><em>EvtDmaEnablerDisable (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)"><em>EvtDmaEnablerFlush (KMDF </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)"><em>) EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)"><em>EvtInterruptDisable</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a> (<strong>WdfPowerDeviceD3Final</strong> state) <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)"><em>EvtDeviceReleaseHardware</em></a>
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> (<strong>WdfRequestStopActionPurge</strong> EvtDeviceSelfManagedIoFlush <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)"><em>EvtDeviceSelfManagedIoFlush</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mn-write-config" data-raw-source="[&lt;strong&gt;IRP_MN_WRITE_CONFIG&lt;/strong&gt;](../kernel/irp-mn-write-config.md)"><strong>IRP_MN_WRITE_CONFIG</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用 <strong>WdfDeviceInitXxx</strong> 方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
</tbody>
</table>

 

## <a name="kmdf-callbacks-for-irp_mj_power"></a>IRP \_ MJ POWER 的 KMDF \_ 回调


下表按执行顺序列出了对应于 [**IRP \_ MJ \_ 功能**](../kernel/irp-mj-power.md)的次要 IRP 代码的 KMDF 回调。 箭头指示 WDM FDO 在传播到堆栈时是否处理 IRP。

**注意**   注意：在 KMDF 驱动程序中，即插即用和电源管理是集成的操作，驱动程序不会收到单个次要 [**IRP \_ mj \_ PNP**](../kernel/irp-mj-pnp.md) 或 [**IRP \_ mj \_ power**](../kernel/irp-mj-power.md) 请求。 相反，框架在开机时调用一组核心回调，并在关闭时调用相应的设置，并在此核心集之前和之后调用其他每个即插即用请求的回调。 有关显示通电和关机顺序的综合关系图，请参阅 [移植 PnP 和电源管理功能](porting-pnp-and-power-management-functionality.md)。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IRP_MJ_POWER 次要代码</th>
<th align="left">框架回调</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](../kernel/irp-mn-set-power.md)"><strong>IRP_MN_SET_POWER</strong></a> 用于 D1、D2 或 D3 (关闭) </td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> (<strong>WdfRequestStopActionSuspend</strong>标志) <a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromS0&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)"><em>EvtDeviceArmWakeFromS0</em></a>或<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSx&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)"><em>EvtDeviceArmWakeFromSx</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)"><em>EvtDmaEnablerSelfManagedIoStop (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)"><em>EvtDmaEnablerDisable (</em></a>KMDF 仅) EvtDmaEnablerFlush (KMDF
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)"><em>仅</em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)"><em>) EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)"><em>EvtInterruptDisable</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a></td>
</tr>
<tr class="even">
<td align="left">用于 D0 (通电) 的↑<a href="/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](../kernel/irp-mn-set-power.md)"><strong>IRP_MN_SET_POWER</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EvtDeviceD0Entry</em></a>
<a href="/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)"><em>EvtInterruptEnable</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)"><em>EVTDMAENABLERFILL (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)"><em>EvtDmaEnablerEnable (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)"><em>EvtDmaEnablerSelfManagedIoStart (KMDF 仅) </em></a> 
<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>EvtIoResume</em></a>
<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)"><em>EvtDeviceSelfManagedIoRestart</em></a></td>
</tr>
<tr class="odd">
<td align="left">Sx 的↓<a href="/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](../kernel/irp-mn-set-power.md)"><strong>IRP_MN_SET_POWER</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">Sx 的↑<a href="/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](../kernel/irp-mn-set-power.md)"><strong>IRP_MN_SET_POWER</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/kernel/irp-mn-power-sequence" data-raw-source="[&lt;strong&gt;IRP_MN_POWER_SEQUENCE&lt;/strong&gt;](../kernel/irp-mn-power-sequence.md)"><strong>IRP_MN_POWER_SEQUENCE</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">↓<a href="/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](../kernel/irp-mn-wait-wake.md)"><strong>IRP_MN_WAIT_WAKE</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)"><em>EvtDeviceEnableWakeAtBus (KMDF 仅) </em></a></td>
</tr>
<tr class="odd">
<td align="left">↑<a href="/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](../kernel/irp-mn-wait-wake.md)"><strong>IRP_MN_WAIT_WAKE</strong></a></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus (KMDF only)&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)"><em>EvtDeviceDisableWakeAtBus (KMDF 仅) </em></a></td>
</tr>
</tbody>
</table>

 


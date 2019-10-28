---
title: WDM Irp 和 WDF 事件回调函数
description: WDM Irp 和 WDF 事件回调函数
ms.assetid: 9B9A01FD-AA15-4C30-B19D-2F6451014EAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74a0b357ba1ca6aa7bb812eb15ca7b7b5dd1bec8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842791"
---
# <a name="wdm-irps-and-wdf-event-callback-functions"></a>WDM Irp 和 WDF 事件回调函数


内核模式驱动程序框架（KMDF）和用户模式驱动程序框架（UMDF）支持一部分 Windows Irp。 下表列出了主要的 WDM IRP 类型和相应的框架事件回调函数。 除非另外指定，否则回调同时适用于 KMDF 和 UMDF。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)"><strong>IRP_MJ_CLEANUP</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup" data-raw-source="[&lt;em&gt;EvtFileCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)"><em>EvtFileCleanup</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close" data-raw-source="[&lt;strong&gt;IRP_MJ_CLOSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)"><strong>IRP_MJ_CLOSE</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close" data-raw-source="[&lt;em&gt;EvtFileClose&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)"><em>EvtFileClose</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)"><strong>IRP_MJ_CREATE</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create" data-raw-source="[&lt;em&gt;EvtDeviceFileCreate&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)"><em>EvtDeviceFileCreate</em></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="even">
<td align="left">IRP_MJ_CREATE_MAILSLOT</td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left">IRP_MJ_DEVICE_CHANGE</td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DIRECTORY_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)"><strong>IRP_MJ_DIRECTORY_CONTROL</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-file-system-control" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-file-system-control)"><strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers" data-raw-source="[&lt;strong&gt;IRP_MJ_FLUSH_BUFFERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)"><strong>IRP_MJ_FLUSH_BUFFERS</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)"><strong>IRP_MJ_LOCK_CONTROL</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp" data-raw-source="[&lt;strong&gt;IRP_MJ_PNP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)"><strong>IRP_MJ_PNP</strong></a></td>
<td align="left">多年请参阅<a href="#kmdf-callbacks-for-irp_mj_pnp" data-raw-source="[KMDF Callbacks for IRP_MJ_PNP](#kmdf-callbacks-for-irp_mj_pnp)">IRP_MJ_PNP 的 KMDF 回调</a>。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)"><strong>IRP_MJ_POWER</strong></a></td>
<td align="left">多年请参阅<a href="#kmdf-callbacks-for-irp_mj_power" data-raw-source="[KMDF Callbacks for IRP_MJ_POWER](#kmdf-callbacks-for-irp_mj_power)">IRP_MJ_POWER 的 KMDF 回调</a>。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_EA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)"><strong>IRP_MJ_QUERY_EA</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)"><strong>IRP_MJ_QUERY_INFORMATION</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)"><strong>IRP_MJ_QUERY_QUOTA</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_SECURITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)"><strong>IRP_MJ_QUERY_SECURITY</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)"><strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)"><strong>IRP_MJ_READ</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_EA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)"><strong>IRP_MJ_SET_EA</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)"><strong>IRP_MJ_SET_INFORMATION</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_QUOTA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)"><strong>IRP_MJ_SET_QUOTA</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_SECURITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)"><strong>IRP_MJ_SET_SECURITY</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)"><strong>IRP_MJ_SET_VOLUME_INFORMATION</strong></a></td>
<td align="left">无直接支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"> <em>EvtDeviceWdmIrpPreprocess （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown" data-raw-source="[&lt;strong&gt;IRP_MJ_SHUTDOWN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)"><strong>IRP_MJ_SHUTDOWN</strong></a></td>
<td align="left"><p>对于控制设备对象，实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nc-wdfcontrol-evt_wdf_device_shutdown_notification" data-raw-source="[&lt;em&gt;EvtDeviceShutdownNotification (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nc-wdfcontrol-evt_wdf_device_shutdown_notification)"> <em>EvtDeviceShutdownNotification （仅限 KMDF）</em></a></p>
<p>对于所有即插即用设备对象：不支持;实现<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>EvtDeviceWdmIrpPreprocess （仅适用于 KMDF）</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control" data-raw-source="[&lt;strong&gt;IRP_MJ_SYSTEM_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)"><strong>IRP_MJ_SYSTEM_CONTROL</strong></a></td>
<td align="left">创建 WDFWMIPROVIDER 和 WDFWMIINSTANCE 对象，并实现<strong>EvtWmiXxx （仅限 KMDF）</strong>回调。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)"><strong>IRP_MJ_WRITE</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a></td>
</tr>
</tbody>
</table>

 

## <a name="kmdf-callbacks-for-irp_mj_pnp"></a>IRP\_MJ\_PNP 的 KMDF 回调


下表按执行顺序列出了对应于[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)的次要 IRP 代码的 KMDF 回调。 箭头指示 WDM FDO 在传播到堆栈时是否处理 IRP。

**请注意**   在 KMDF 驱动程序中，即插即用和电源管理是集成的操作，驱动程序不会接收单独的次要[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)或 IRP\_的[**power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)请求\_ 相反，框架在开机时调用一组核心回调，并在关闭时调用相应的设置，并在此核心集之前和之后调用其他每个即插即用请求的回调。 有关显示通电和关机顺序的综合关系图，请参阅[移植 PnP 和电源管理功能](porting-pnp-and-power-management-functionality.md)。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IRP_MJ_PNP 次代码</th>
<th align="left">KMDF 回调</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device" data-raw-source="[&lt;strong&gt;IRP_MN_CANCEL_REMOVE_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)"><strong>IRP_MN_CANCEL_REMOVE_DEVICE</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device" data-raw-source="[&lt;strong&gt;IRP_MN_CANCEL_STOP_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)"><strong>IRP_MN_CANCEL_STOP_DEVICE</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="odd">
<td align="left">↑<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification" data-raw-source="[&lt;strong&gt;IRP_MN_DEVICE_USAGE_NOTIFICATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)"><strong>IRP_MN_DEVICE_USAGE_NOTIFICATION</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification" data-raw-source="[&lt;em&gt;EvtDeviceUsageNotification&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification)"><em>EvtDeviceUsageNotification</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-eject" data-raw-source="[&lt;strong&gt;IRP_MN_EJECT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-eject)"><strong>IRP_MN_EJECT</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject" data-raw-source="[&lt;em&gt;EvtDeviceEject (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_eject)"><em>EvtDeviceEject （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements" data-raw-source="[&lt;strong&gt;IRP_MN_FILTER_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)"><strong>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements" data-raw-source="[&lt;em&gt;EvtDeviceFilterRemoveResourceRequirements (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)"><em>EvtDeviceFilterRemoveResourceRequirements （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left">↑<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements" data-raw-source="[&lt;strong&gt;IRP_MN_FILTER_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)"><strong>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements" data-raw-source="[&lt;em&gt;EvtDeviceFilterAddResourceRequirements (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)"><em>EvtDeviceFilterAddResourceRequirements （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_BUS_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)"><strong>IRP_MN_QUERY_BUS_INFORMATION</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)"><strong>IRP_MN_QUERY_CAPABILITIES</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_DEVICE_RELATIONS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)"><strong>IRP_MN_QUERY_DEVICE_RELATIONS</strong></a> （总线、删除和弹出关系）</td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_relations_query" data-raw-source="[&lt;em&gt;EvtDeviceRelationsQuery&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_relations_query)"><em>EvtDeviceRelationsQuery</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_DEVICE_TEXT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)"><strong>IRP_MN_QUERY_DEVICE_TEXT</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)"><strong>IRP_MN_QUERY_ID</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)"><strong>IRP_MN_QUERY_INTERFACE</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request" data-raw-source="[&lt;em&gt;EvtDeviceProcessQueryInterfaceRequest (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfqueryinterface/nc-wdfqueryinterface-evt_wdf_device_process_query_interface_request)"><em>EvtDeviceProcessQueryInterfaceRequest （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_PNP_DEVICE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state)"><strong>IRP_MN_QUERY_PNP_DEVICE_STATE</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_REMOVE_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)"><strong>IRP_MN_QUERY_REMOVE_DEVICE</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove" data-raw-source="[&lt;em&gt;EvtDeviceQueryRemove&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)"><em>EvtDeviceQueryRemove</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)"><strong>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query)"><em>EvtDeviceResourceRequirementsQuery （仅限 KMDF）</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources)"><strong>IRP_MN_QUERY_RESOURCES</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)"><em>EvtDeviceResourcesQuery （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_STOP_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)"><strong>IRP_MN_QUERY_STOP_DEVICE</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop" data-raw-source="[&lt;em&gt;EvtDeviceQueryStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)"><em>EvtDeviceQueryStop</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config" data-raw-source="[&lt;strong&gt;IRP_MN_READ_CONFIG&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)"><strong>IRP_MN_READ_CONFIG</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device" data-raw-source="[&lt;strong&gt;IRP_MN_REMOVE_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)"><strong>IRP_MN_REMOVE_DEVICE</strong></a></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_REMOVE_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)"><strong>IRP_MN_QUERY_REMOVE_DEVICE</strong></a>之后：</p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> （<strong>WdfRequestStopActionSuspend</strong>标志） <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)"><em>EvtDmaEnablerSelfManagedIoStop （仅限 KMDF</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)"><em>） EvtDmaEnablerDisable</em></a>（仅限
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)"><em>KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)"><em>EvtInterruptDisable</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a> （<strong>WdfPowerDeviceD3Final</strong> state） <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)"><em>EvtDeviceReleaseHardware</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> （<strong>WdfRequestStopActionPurge</strong>标志），适用于非电源管理的队列的电源管理队列<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)"><em>EvtDeviceSelfManagedIoFlush</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> （<strong>WdfRequestStopActionPurge</strong>标志） <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)"><em>EvtDeviceSelfManagedIoCleanup</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)"><em>EvtCleanupCallback</em></a> For WDFDEVICE <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)"><em>EvtDestroyCallback</em></a> for WDFDEVICE
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)"><strong>IRP_MN_SURPRISE_REMOVAL</strong></a>之后：</p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> （<strong>WdfRequestStopActionPurge</strong>标志），适用于非电源管理队列<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)"><em>EvtDeviceSelfManagedIoCleanup</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)"><em>EvtCleanupCallback</em></a> for WDFDEVICE <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)"><em>EvtDestroyCallback</em></a> for WDFDEVICE</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock" data-raw-source="[&lt;strong&gt;IRP_MN_SET_LOCK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-lock)"><strong>IRP_MN_SET_LOCK</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock" data-raw-source="[&lt;em&gt;EvtDeviceSetLock (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_set_lock)"><em>EvtDeviceSetLock （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left">↑<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device" data-raw-source="[&lt;strong&gt;IRP_MN_START_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)"><strong>IRP_MN_START_DEVICE</strong></a></td>
<td align="left"><p>枚举后：</p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)"><em>EvtDeviceRemoveAddedResources （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EvtDeviceD0Entry</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)"><em>EvtInterruptEnable</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)"><em>EvtDmaEnablerFill （仅限 KMDF）</em></a> 
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)"><em>EvtDmaEnablerEnable （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)"><em>EvtDmaEnablerSelfManagedIoStart （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoInit&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)"><em>EvtDeviceSelfManagedIoInit</em></a>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device" data-raw-source="[&lt;strong&gt;IRP_MN_STOP_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)"><strong>IRP_MN_STOP_DEVICE</strong></a>之后：</p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_remove_added_resources)"><em>EvtDeviceRemoveAddedResources （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EvtDeviceD0Entry</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)"><em>EvtInterruptEnable</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)"><em>EvtDmaEnablerFill （仅限 KMDF）</em></a> 
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)"><em>EvtDmaEnablerEnable （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)"><em>EvtDmaEnablerSelfManagedIoStart （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>EvtIoResume</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)"><em>EvtDeviceSelfManagedIoRestart</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device" data-raw-source="[&lt;strong&gt;IRP_MN_STOP_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)"><strong>IRP_MN_STOP_DEVICE</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> （<strong>WdfRequestStopActionSuspend</strong>标志） <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)"><em>EvtDmaEnablerSelfManagedIoStop （仅限 KMDF</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)"><em>） EvtDmaEnablerDisable</em></a>（仅限
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)"><em>KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)"><em>EvtInterruptDisable</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a> （<strong>WdfPowerDeviceD3Final</strong> state） <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)"><em>EvtDeviceReleaseHardware</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)"><strong>IRP_MN_SURPRISE_REMOVAL</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"><em>EvtDeviceSurpriseRemoval</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> （<strong>WDFREQUESTSTOPACTIONSUSPEND</strong>标志） <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)"><em>EvtDmaEnablerSelfManagedIoStop （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)"><em>EvtDmaEnablerDisable （仅限 KMDF）</em></a> 
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)"><em>EvtDmaEnablerFlush （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)"><em>EvtInterruptDisable</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a> （<strong>WdfPowerDeviceD3Final</strong> state） <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)"><em>EvtDeviceReleaseHardware</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)"><em>EvtDeviceSelfManagedIoFlush</em></a>的<strong>WdfRequestStopActionPurge</strong>标志</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config" data-raw-source="[&lt;strong&gt;IRP_MN_WRITE_CONFIG&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)"><strong>IRP_MN_WRITE_CONFIG</strong></a></td>
<td align="left">无。 KMDF 驱动程序调用<strong>WdfDeviceInitXxx</strong>方法来设置在初始化期间的设备属性，以便框架能够自行响应此查询，而不会通知驱动程序。</td>
</tr>
</tbody>
</table>

 

## <a name="kmdf-callbacks-for-irp_mj_power"></a>用于 IRP\_MJ\_POWER 的 KMDF 回调


下表按执行顺序列出了对应于[**IRP\_MJ\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)的次要 irp 代码的 KMDF 回调。 箭头指示 WDM FDO 在传播到堆栈时是否处理 IRP。

**注意**   注意：在 KMDF 驱动程序中，即插即用和电源管理是集成的操作，驱动程序不会接收单个次要 IRP [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) [ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)\_ 相反，框架在开机时调用一组核心回调，并在关闭时调用相应的设置，并在此核心集之前和之后调用其他每个即插即用请求的回调。 有关显示通电和关机顺序的综合关系图，请参阅[移植 PnP 和电源管理功能](porting-pnp-and-power-management-functionality.md)。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IRP_MJ_POWER 次代码</th>
<th align="left">框架回调</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)"><strong>IRP_MN_SET_POWER</strong></a> for D1、D2 或 D3 （断电）</td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a> （<strong>WdfRequestStopActionSuspend</strong>标志） <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromS0&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)"><em>EVTDEVICEARMWAKEFROMS0</em></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)"><em>EvtDeviceArmWakeFromSx</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)"><em>EvtDmaEnablerSelfManagedIoStop （仅限 KMDF）</em></a> 
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable)"><em>EvtDmaEnablerDisable （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)"><em>EvtDmaEnablerFlush （仅限 KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)"><em>EvtInterruptDisable</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)"><em>EvtDeviceD0Exit</em></a></td>
</tr>
<tr class="even">
<td align="left">↑<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)"><strong>IRP_MN_SET_POWER</strong></a> for D0 （通电）</td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EvtDeviceD0Entry</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)"><em>EvtInterruptEnable</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)"><em>EVTDEVICED0ENTRYPOSTINTERRUPTSENABLED</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)"><em>EvtDmaEnablerFill （</em></a>仅限 KMDF）
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)"><em>EvtDmaEnablerEnable</em></a>（仅限
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)"><em>KMDF）</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>EvtIoResume</em></a>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)"><em>EvtDeviceSelfManagedIoRestart</em></a></td>
</tr>
<tr class="odd">
<td align="left">Sx 的↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)"><strong>IRP_MN_SET_POWER</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">Sx 的↑<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)"><strong>IRP_MN_SET_POWER</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence" data-raw-source="[&lt;strong&gt;IRP_MN_POWER_SEQUENCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)"><strong>IRP_MN_POWER_SEQUENCE</strong></a></td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)"><strong>IRP_MN_WAIT_WAKE</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus)"><em>EvtDeviceEnableWakeAtBus （仅限 KMDF）</em></a></td>
</tr>
<tr class="odd">
<td align="left">↑<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)"><strong>IRP_MN_WAIT_WAKE</strong></a></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus (KMDF only)&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)"><em>EvtDeviceDisableWakeAtBus （仅限 KMDF）</em></a></td>
</tr>
</tbody>
</table>

 

 

 






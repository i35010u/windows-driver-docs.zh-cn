---
title: DDI 用法规则集 (KMDF)
description: 使用这些规则验证驱动程序是否正确地使用了 KMDF DDIs。
ms.assetid: 0A3A012C-A1BB-43A5-B38D-4E98928D07E5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcf3039d7773c806b3124220e4b70857c8286d94
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384067"
---
# <a name="ddi-usage-rule-set-kmdf"></a>DDI 用法规则集 (KMDF)


使用这些规则验证驱动程序是否正确地使用了 KMDF DDIs。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedioctl.md)"><strong>BufAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedioctl.md)"><strong>BufAfterReqCompletedIoctl</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a>回调函数中，在 i/o 请求完成后，无法访问检索到的 i/o 请求缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctl.md)"><strong>BufAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctl.md)"><strong>BufAfterReqCompletedIntIoctl</strong></a>规则指定在请求完成后，不能)  (在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a>回调函数内访问其缓冲区。 通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveOutputBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)"><strong>WdfRequestRetrieveOutputBuffer</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserOutputBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)"><strong>WdfRequestRetrieveUnsafeUserOutputBuffer</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveInputBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)"><strong>WdfRequestRetrieveInputBuffer</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserInputBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)"><strong>WdfRequestRetrieveUnsafeUserInputBuffer</strong></a>来检索缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctla.md)"><strong>BufAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctla.md)"><strong>BufAfterReqCompletedIntIoctlA</strong></a>规则验证请求完成后，不能)  (在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a>回调中访问其缓冲区。 通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveInputBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)"><strong>WdfRequestRetrieveInputBuffer</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveOutputBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)"><strong>WdfRequestRetrieveOutputBuffer</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserInputBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)"><strong>WdfRequestRetrieveUnsafeUserInputBuffer</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserOutputBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)"><strong>WdfRequestRetrieveUnsafeUserOutputBuffer</strong></a>检索到了缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedioctla.md)"><strong>BufAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedioctla.md)"><strong>BufAfterReqCompletedIoctlA</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a>回调函数中，在 i/o 请求完成后，无法访问检索到的 i/o 请求缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedRead&lt;/strong&gt;](kmdf-bufafterreqcompletedread.md)"><strong>BufAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedRead&lt;/strong&gt;](kmdf-bufafterreqcompletedread.md)"><strong>BufAfterReqCompletedRead</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>回调函数中，在 i/o 请求完成后，无法访问检索到的 i/o 请求缓冲区。 有14个 DDIs 充当可能的缓冲区访问方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedReadA&lt;/strong&gt;](kmdf-bufafterreqcompletedreada.md)"><strong>BufAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedReadA 规则指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a> 回调函数中，在 i/o 请求完成后，无法访问检索到的 i/o 请求缓冲区。 有14个 DDIs 充当可能的缓冲区访问方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedWrite&lt;/strong&gt;](kmdf-bufafterreqcompletedwrite.md)"><strong>BufAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedWrite 规则指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a> 回调函数中，在 i/o 请求完成后，无法访问检索到的 i/o 请求缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-bufafterreqcompletedwritea.md)"><strong>BufAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedWriteA 规则指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a> 回调函数中，在 i/o 请求完成后，无法访问检索到的 i/o 请求缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-childdeviceinitapi.md" data-raw-source="[&lt;strong&gt;ChildDeviceInitApi&lt;/strong&gt;](kmdf-childdeviceinitapi.md)"><strong>ChildDeviceInitApi</strong></a></p></td>
<td align="left"><p><a href="kmdf-childdeviceinitapi.md" data-raw-source="[&lt;strong&gt;ChildDeviceInitApi&lt;/strong&gt;](kmdf-childdeviceinitapi.md)"><strong>ChildDeviceInitApi</strong></a>规则指定对于子设备，必须在驱动程序为子设备对象调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>方法之前调用框架设备对象初始化方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-controldevicedeleted.md" data-raw-source="[&lt;strong&gt;ControlDeviceDeleted&lt;/strong&gt;](kmdf-controldevicedeleted.md)"><strong>ControlDeviceDeleted</strong></a></p></td>
<td align="left"><p>ControDeviceDeleted 规则指定如果 PnP 驱动程序创建控制设备对象，则驱动程序必须在卸载该驱动程序之前，在某个清除回调函数中删除该控制设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-controldeviceinitapi.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAPI&lt;/strong&gt;](kmdf-controldeviceinitapi.md)"><strong>ControlDeviceInitAPI</strong></a></p></td>
<td align="left"><p>ControlDeviceInitAPI 规则指定必须先调用设置控制设备<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](../wdf/wdfdevice_init.md)"><strong>WDFDEVICE_INIT</strong></a>结构的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>WdfControlDeviceInitAllocate</strong></a>和所有其他设备对象初始化 DDIs，然后才能<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>控制设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-ctldevicefinishinitdeviceadd.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDeviceAdd&lt;/strong&gt;](kmdf-ctldevicefinishinitdeviceadd.md)"><strong>CtlDeviceFinishInitDeviceAdd</strong></a></p></td>
<td align="left"><p><a href="kmdf-ctldevicefinishinitdeviceadd.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDeviceAdd&lt;/strong&gt;](kmdf-ctldevicefinishinitdeviceadd.md)"><strong>CtlDeviceFinishInitDeviceAdd</strong></a>规则指定如果驱动程序在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"><em>EvtDriverDeviceAdd</em></a>回调函数中创建控制设备对象，则它必须在创建设备后、从<strong>EvtDriverDeviceAdd</strong>回调函数退出之前调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing" data-raw-source="[&lt;strong&gt;WdfControlFinishInitializing&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)"><strong>WdfControlFinishInitializing</strong></a> 。 此规则不适用于非 PnP 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-ctldevicefinishinitdrentry.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDrEntry&lt;/strong&gt;](kmdf-ctldevicefinishinitdrentry.md)"><strong>CtlDeviceFinishInitDrEntry</strong></a></p></td>
<td align="left"><p>CtlDeviceFinishInitDrEntry 规则指定如果驱动程序在<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](../wdf/driverentry-for-kmdf-drivers.md)"><strong>DriverEntry</strong></a>回调函数中创建控制设备对象，则该对象必须在创建设备后、从<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"><em>EvtDriverDeviceAdd</em></a>回调函数退出之前调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing" data-raw-source="[&lt;strong&gt;WdfControlFinishInitializing&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)"><strong>WdfControlFinishInitializing</strong></a> 。 此规则不适用于非 PnP 驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-devicecreatefail.md" data-raw-source="[&lt;strong&gt;DeviceCreateFail&lt;/strong&gt;](kmdf-devicecreatefail.md)"><strong>DeviceCreateFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-devicecreatefail.md" data-raw-source="[&lt;strong&gt;DeviceCreateFail&lt;/strong&gt;](kmdf-devicecreatefail.md)"><strong>DeviceCreateFail</strong></a>规则指定在对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>的调用失败时，EVT_WDF_DRIVER_DEVICE_ADD 返回错误状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-deviceinitallocate.md" data-raw-source="[&lt;strong&gt;DeviceInitAllocate&lt;/strong&gt;](kmdf-deviceinitallocate.md)"><strong>DeviceInitAllocate</strong></a></p></td>
<td align="left"><p><a href="kmdf-deviceinitallocate.md" data-raw-source="[&lt;strong&gt;DeviceInitAllocate&lt;/strong&gt;](kmdf-deviceinitallocate.md)"><strong>DeviceInitAllocate</strong></a>规则指定，对于 PDO 设备或控制设备对象，必须在驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>之前调用框架设备对象初始化方法<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"><strong>WdfPdoInitAllocate</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>WdfControlDeviceInitAllocate</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-deviceinitapi.md" data-raw-source="[&lt;strong&gt;DeviceInitAPI&lt;/strong&gt;](kmdf-deviceinitapi.md)"><strong>DeviceInitAPI</strong></a></p></td>
<td align="left"><p>对于 FDO 设备，必须先调用框架设备对象初始化方法和框架 FDO 初始化方法，然后再调用设备对象的 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a> 方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-doubledeviceinitfree.md" data-raw-source="[&lt;strong&gt;DoubleDeviceInitFree&lt;/strong&gt;](kmdf-doubledeviceinitfree.md)"><strong>DoubleDeviceInitFree</strong></a></p></td>
<td align="left"><p><a href="kmdf-doubledeviceinitfree.md" data-raw-source="[&lt;strong&gt;DoubleDeviceInitFree&lt;/strong&gt;](kmdf-doubledeviceinitfree.md)"><strong>DoubleDeviceInitFree</strong></a>规则指定驱动程序不应释放设备初始化结构两次。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-drivercreate.md" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](kmdf-drivercreate.md)"><strong>DriverCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-drivercreate.md" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](kmdf-drivercreate.md)"><strong>DriverCreate</strong></a>规则指定使用内核模式驱动程序框架 (KMDF) 的驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate" data-raw-source="[&lt;strong&gt;WdfDriverCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)"><strong>WdfDriverCreate</strong></a>方法，以便在其<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](../wdf/driverentry-for-kmdf-drivers.md)"><strong>DriverEntry</strong></a>例程中创建框架驱动程序对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreedevicecallback.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCallback&lt;/strong&gt;](kmdf-initfreedevicecallback.md)"><strong>InitFreeDeviceCallback</strong></a></p></td>
<td align="left"><p>InitFreeDeviceCallback 规则指定如果驱动程序在初始化新框架设备对象时遇到错误，并且驱动程序在调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>WdfControlDeviceInitAllocate</strong></a>接收到<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](../wdf/wdfdevice_init.md)"><strong>WDFDEVICE_INIT</strong></a>结构时，必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>WdfDeviceInitFree</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-initfreedevicecreate.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreate&lt;/strong&gt;](kmdf-initfreedevicecreate.md)"><strong>InitFreeDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreedevicecreate.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreate&lt;/strong&gt;](kmdf-initfreedevicecreate.md)"><strong>InitFreeDeviceCreate</strong></a>规则指定如果某个设备对象初始化方法中出现错误，并且驱动程序从对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>WdfControlDeviceInitAllocate</strong></a>的调用接收到<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](../wdf/wdfdevice_init.md)"><strong>WDFDEVICE_INIT</strong></a>结构，则驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>WdfDeviceInitFree</strong></a>而不是<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreedevicecreatetype2.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType2&lt;/strong&gt;](kmdf-initfreedevicecreatetype2.md)"><strong>InitFreeDeviceCreateType2</strong></a></p></td>
<td align="left"><p>InitFreeDeviceCreateType2 规则指定驱动程序在调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>WdfDeviceInitFree</strong></a>后不得调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-initfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-initfreedevicecreatetype4.md)"><strong>InitFreeDeviceCreateType4</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-initfreedevicecreatetype4.md)"><strong>InitFreeDeviceCreateType4</strong></a>规则指定如果驱动程序在调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>时遇到错误，则驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>WdfDeviceInitFree</strong></a> ，并且如果驱动程序从对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>WdfControlDeviceInitAllocate</strong></a>的调用接收到<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](../wdf/wdfdevice_init.md)"><strong>WDFDEVICE_INIT</strong></a>结构，则为。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreenull.md" data-raw-source="[&lt;strong&gt;InitFreeNull&lt;/strong&gt;](kmdf-initfreenull.md)"><strong>InitFreeNull</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreenull.md" data-raw-source="[&lt;strong&gt;InitFreeNull&lt;/strong&gt;](kmdf-initfreenull.md)"><strong>InitFreeNull</strong></a>规则指定无法使用指向<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[WDFDEVICE_INIT](../wdf/wdfdevice_init.md)">WDFDEVICE_INIT</a>结构的<strong>NULL</strong>指针调用作为参数接收 PWDFDEVICE_INIT。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctl.md)"><strong>MdlAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p>MdlAfterReqCompletedIntIoctl 规则指定在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a> 回调函数中，内存描述符列表 (MDL) 在 i/o 请求完成后无法访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctla.md)"><strong>MdlAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctla.md)"><strong>MdlAfterReqCompletedIntIoctlA</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a>回调函数中，内存描述符列表 (MDL) 在 i/o 请求完成后无法访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctl.md)"><strong>MdlAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctl.md)"><strong>MdlAfterReqCompletedIoctl</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a>回调函数中，内存描述符列表 (MDL) 在 i/o 请求完成后无法访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctla.md)"><strong>MdlAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctla.md)"><strong>MdlAfterReqCompletedIoctlA</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a>回调函数中，内存描述符列表 (MDL) 在 i/o 请求完成后无法访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedRead&lt;/strong&gt;](kmdf-mdlafterreqcompletedread.md)"><strong>MdlAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedRead&lt;/strong&gt;](kmdf-mdlafterreqcompletedread.md)"><strong>MdlAfterReqCompletedRead</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>回调函数中， (MDL) 对象的内存描述符列表无法在 i/o 请求完成后访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedReadA&lt;/strong&gt;](kmdf-mdlafterreqcompletedreada.md)"><strong>MdlAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedReadA&lt;/strong&gt;](kmdf-mdlafterreqcompletedreada.md)"><strong>MdlAfterReqCompletedReadA</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>回调函数中， (MDL) 对象的内存描述符列表无法在 i/o 请求完成后访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWrite&lt;/strong&gt;](kmdf-mdlafterreqcompletedwrite.md)"><strong>MdlAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWrite&lt;/strong&gt;](kmdf-mdlafterreqcompletedwrite.md)"><strong>MdlAfterReqCompletedWrite</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a>回调函数中， (MDL) 对象的内存描述符列表无法在 i/o 请求完成后访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-mdlafterreqcompletedwritea.md)"><strong>MdlAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-mdlafterreqcompletedwritea.md)"><strong>MdlAfterReqCompletedWriteA</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a>回调函数中， (MDL) 对象的内存描述符列表无法在 i/o 请求完成后访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedintioctl.md)"><strong>MemAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedintioctl.md)"><strong>MemAfterReqCompletedIntIoctl</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a>回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedintioctla.md)"><strong>MemAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedintioctla.md)"><strong>MemAfterReqCompletedIntIoctlA</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>EvtIoInternalDeviceControl</em></a>回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedioctl.md)"><strong>MemAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedioctl.md)"><strong>MemAfterReqCompletedIoctl</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a>回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedioctla.md)"><strong>MemAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedioctla.md)"><strong>MemAfterReqCompletedIoctlA</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>EvtIoDeviceControl</em></a>回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedRead&lt;/strong&gt;](kmdf-memafterreqcompletedread.md)"><strong>MemAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedRead&lt;/strong&gt;](kmdf-memafterreqcompletedread.md)"><strong>MemAfterReqCompletedRead</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](kmdf-memafterreqcompletedreada.md)"><strong>MemAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](kmdf-memafterreqcompletedreada.md)"><strong>MemAfterReqCompletedReadA</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWrite&lt;/strong&gt;](kmdf-memafterreqcompletedwrite.md)"><strong>MemAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWrite&lt;/strong&gt;](kmdf-memafterreqcompletedwrite.md)"><strong>MemAfterReqCompletedWrite</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a>回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-memafterreqcompletedwritea.md)"><strong>MemAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-memafterreqcompletedwritea.md)"><strong>MemAfterReqCompletedWriteA</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a>回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullcheck.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheck.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 规则验证驱动程序代码中的 NULL 值是否在稍后的驱动程序中未被引用。 如果满足以下任一条件，则此规则将报告缺陷：</p>
<ul>
<li>指定的值为 NULL，稍后取消引用。</li>
<li>驱动程序中有一个全局/参数，该过程在后面可能为 NULL 的情况下，在该驱动程序中有一个明确的检查，表示指针的初始值可能为 NULL。</li>
</ul>
<p>对于 NullCheck 规则冲突，最相关的代码语句在跟踪树窗格中突出显示。 有关使用报表输出的详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report" data-raw-source="[Static Driver Verifier Report](./static-driver-verifier-report.md)">静态驱动程序验证程序报表</a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer" data-raw-source="[Understanding the Trace Viewer](./understanding-the-defect-viewer.md)">了解跟踪查看器</a>。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdodeviceinitapi.md" data-raw-source="[&lt;strong&gt;PdoDeviceInitAPI&lt;/strong&gt;](kmdf-pdodeviceinitapi.md)"><strong>PdoDeviceInitAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdodeviceinitapi.md" data-raw-source="[&lt;strong&gt;PdoDeviceInitAPI&lt;/strong&gt;](kmdf-pdodeviceinitapi.md)"><strong>PdoDeviceInitAPI</strong></a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"><strong>WdfPdoInitAllocate</strong></a>和所有其他设备对象初始化 DDIs，用于为物理设备对象 (pdo) 设置<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](../wdf/wdfdevice_init.md)"><strong>WDFDEVICE_INIT</strong></a>结构，然后才能调用 pdo 的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecallback.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCallback&lt;/strong&gt;](kmdf-pdoinitfreedevicecallback.md)"><strong>PdoInitFreeDeviceCallback</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdoinitfreedevicecallback.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCallback&lt;/strong&gt;](kmdf-pdoinitfreedevicecallback.md)"><strong>PdoInitFreeDeviceCallback</strong></a>规则指定当驱动程序调用任何框架设备对象初始化函数时，驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>WdfDeviceInitFree</strong></a> （如果出现错误）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreate.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreate&lt;/strong&gt;](kmdf-pdoinitfreedevicecreate.md)"><strong>PdoInitFreeDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreate.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreate&lt;/strong&gt;](kmdf-pdoinitfreedevicecreate.md)"><strong>PdoInitFreeDeviceCreate</strong></a>规则指定如果某个设备对象初始化函数中出现错误，并且驱动程序从对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"><strong>WdfPdoInitAllocate</strong></a>的调用接收到 WDFDEVICE_INIT 结构，则驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>WdfDeviceInitFree</strong></a>而不是<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreatetype2.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreateType2&lt;/strong&gt;](kmdf-pdoinitfreedevicecreatetype2.md)"><strong>PdoInitFreeDeviceCreateType2</strong></a></p></td>
<td align="left"><p>PdoInitFreeDeviceCreateType2 规则指定驱动程序在调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>WdfDeviceInitFree</strong></a>后不得调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-pdoinitfreedevicecreatetype4.md)"><strong>PdoInitFreeDeviceCreateType4</strong></a></p></td>
<td align="left"><p>PdoInitFreeDeviceCreateType4 规则指定如果驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>时出现错误，驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>WdfDeviceInitFree</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-controldeviceinitallocate.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAllocate&lt;/strong&gt;](kmdf-controldeviceinitallocate.md)"><strong>ControlDeviceInitAllocate</strong></a></p></td>
<td align="left"><p><a href="kmdf-controldeviceinitallocate.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAllocate&lt;/strong&gt;](kmdf-controldeviceinitallocate.md)"><strong>ControlDeviceInitAllocate</strong></a>规则指定对于控制设备对象，驱动程序必须先调用框架设备对象初始化方法<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>WdfControlDeviceInitAllocate</strong></a> ，然后才能调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-inputbufferapi.md" data-raw-source="[&lt;strong&gt;InputBufferAPI&lt;/strong&gt;](kmdf-inputbufferapi.md)"><strong>InputBufferAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-inputbufferapi.md" data-raw-source="[&lt;strong&gt;InputBufferAPI&lt;/strong&gt;](kmdf-inputbufferapi.md)"><strong>InputBufferAPI</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>回调函数中使用正确的缓冲区检索 DDIs。 在 <em>EvtIoRead</em> 回调函数中，不能调用以下 DDIs 进行缓冲区检索：</p></td>
</tr>
</tbody>
</table>

 

**选择 DDI 使用规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **DDIUsage**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**DDIUsage。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 


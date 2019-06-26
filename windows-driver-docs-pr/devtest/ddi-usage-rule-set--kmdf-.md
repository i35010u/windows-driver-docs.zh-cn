---
title: DDI 用法规则集 (KMDF)
description: 使用这些规则来验证您的驱动程序正确使用 KMDF DDIs 正确。
ms.assetid: 0A3A012C-A1BB-43A5-B38D-4E98928D07E5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 74a86034ec37b2fe147965dad18ea16875d1aafe
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393239"
---
# <a name="ddi-usage-rule-set-kmdf"></a>DDI 用法规则集 (KMDF)


使用这些规则来验证您的驱动程序正确使用 KMDF DDIs 正确。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedioctl.md)"><strong>BufAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedioctl.md)"> <strong>BufAfterReqCompletedIoctl</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"> <em>EvtIoDeviceControl</em> </a>回调函数，I/O 请求I/O 请求完成后，不能访问检索到的缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctl.md)"><strong>BufAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctl.md)"> <strong>BufAfterReqCompletedIntIoctl</strong> </a>规则指定的请求完成后，无法访问其缓冲区 (内部<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"> <em>EvtIoInternalDeviceControl</em></a>仅回调函数)。 通过调用检索缓冲区<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveOutputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)"> <strong>WdfRequestRetrieveOutputBuffer</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserOutputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)"> <strong>WdfRequestRetrieveUnsafeUserOutputBuffer</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveInputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)"> <strong>WdfRequestRetrieveInputBuffer</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserInputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)"> <strong>WdfRequestRetrieveUnsafeUserInputBuffer</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctla.md)"><strong>BufAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctla.md)"> <strong>BufAfterReqCompletedIntIoctlA</strong> </a>规则验证的请求完成后，无法访问其缓冲区 (内部<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"> <em>EvtIoInternalDeviceControl</em></a>仅回调)。 通过调用检索到缓冲区<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveInputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)"> <strong>WdfRequestRetrieveInputBuffer</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveOutputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)"> <strong>WdfRequestRetrieveOutputBuffer</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserInputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)"> <strong>WdfRequestRetrieveUnsafeUserInputBuffer</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserOutputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)"> <strong>WdfRequestRetrieveUnsafeUserOutputBuffer</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedioctla.md)"><strong>BufAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedioctla.md)"> <strong>BufAfterReqCompletedIoctlA</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"> <em>EvtIoDeviceControl</em> </a>回调函数，I/O 请求I/O 请求完成后，不能访问检索到的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedRead&lt;/strong&gt;](kmdf-bufafterreqcompletedread.md)"><strong>BufAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedRead&lt;/strong&gt;](kmdf-bufafterreqcompletedread.md)"> <strong>BufAfterReqCompletedRead</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"> <em>EvtIoRead</em> </a>回调函数，I/O 请求的缓冲区检索在 I/O 请求完成后，无法访问。 有 14 DDIs 作为可能的缓冲区的访问方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedReadA&lt;/strong&gt;](kmdf-bufafterreqcompletedreada.md)"><strong>BufAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedReadA 规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"> <em>EvtIoRead</em> </a> I/O 请求完成后，无法访问的回调函数，检索到的 I/O 请求缓冲区。 有 14 DDIs 作为可能的缓冲区的访问方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedWrite&lt;/strong&gt;](kmdf-bufafterreqcompletedwrite.md)"><strong>BufAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedWrite 规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"> <em>EvtIoWrite</em> </a> I/O 请求完成后，无法访问的回调函数，检索到的 I/O 请求缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-bufafterreqcompletedwritea.md)"><strong>BufAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedWriteA 规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"> <em>EvtIoWrite</em> </a> I/O 请求完成后，无法访问的回调函数，检索到的 I/O 请求缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-childdeviceinitapi.md" data-raw-source="[&lt;strong&gt;ChildDeviceInitApi&lt;/strong&gt;](kmdf-childdeviceinitapi.md)"><strong>ChildDeviceInitApi</strong></a></p></td>
<td align="left"><p><a href="kmdf-childdeviceinitapi.md" data-raw-source="[&lt;strong&gt;ChildDeviceInitApi&lt;/strong&gt;](kmdf-childdeviceinitapi.md)"> <strong>ChildDeviceInitApi</strong> </a>规则指定，对于子设备，framework 设备对象初始化方法必须在调用之前驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong> </a>子设备对象的方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-controldevicedeleted.md" data-raw-source="[&lt;strong&gt;ControlDeviceDeleted&lt;/strong&gt;](kmdf-controldevicedeleted.md)"><strong>ControlDeviceDeleted</strong></a></p></td>
<td align="left"><p>ControDeviceDeleted 规则指定是否即插即用驱动程序创建一个控制设备对象，该驱动程序必须删除中的一个驱动程序卸载之前清理回调函数的控制设备对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-controldeviceinitapi.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAPI&lt;/strong&gt;](kmdf-controldeviceinitapi.md)"><strong>ControlDeviceInitAPI</strong></a></p></td>
<td align="left"><p>ControlDeviceInitAPI 规则规定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"> <strong>WdfControlDeviceInitAllocate</strong> </a>和所有其他设备对象初始化设置 DDIs <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"> <strong>WDFDEVICE_INIT</strong></a>结构来控制设备必须名为之前<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong> </a>控制设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-ctldevicefinishinitdeviceadd.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDeviceAdd&lt;/strong&gt;](kmdf-ctldevicefinishinitdeviceadd.md)"><strong>CtlDeviceFinishInitDeviceAdd</strong></a></p></td>
<td align="left"><p><a href="kmdf-ctldevicefinishinitdeviceadd.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDeviceAdd&lt;/strong&gt;](kmdf-ctldevicefinishinitdeviceadd.md)"> <strong>CtlDeviceFinishInitDeviceAdd</strong> </a>规则指定如果驱动程序创建控件中的设备对象<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"> <em>EvtDriverDeviceAdd</em> </a>回调函数，它必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing" data-raw-source="[&lt;strong&gt;WdfControlFinishInitializing&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)"> <strong>WdfControlFinishInitializing</strong> </a>创建设备后，退出之前对其从<strong>EvtDriverDeviceAdd</strong>回调函数。 此规则不适用于非 PnP 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-ctldevicefinishinitdrentry.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDrEntry&lt;/strong&gt;](kmdf-ctldevicefinishinitdrentry.md)"><strong>CtlDeviceFinishInitDrEntry</strong></a></p></td>
<td align="left"><p>CtlDeviceFinishInitDrEntry 规则指定如果驱动程序创建中的控制设备对象<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)"> <strong>DriverEntry</strong> </a>回调函数，它必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing" data-raw-source="[&lt;strong&gt;WdfControlFinishInitializing&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)"> <strong>WdfControlFinishInitializing</strong> </a>创建设备后，它从退出之前<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"> <em>EvtDriverDeviceAdd</em> </a>回调函数。 此规则不适用于非 PnP 驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-devicecreatefail.md" data-raw-source="[&lt;strong&gt;DeviceCreateFail&lt;/strong&gt;](kmdf-devicecreatefail.md)"><strong>DeviceCreateFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-devicecreatefail.md" data-raw-source="[&lt;strong&gt;DeviceCreateFail&lt;/strong&gt;](kmdf-devicecreatefail.md)"> <strong>DeviceCreateFail</strong> </a>规则指定 EVT_WDF_DRIVER_DEVICE_ADD 返回了错误状态时调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong> </a>失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-deviceinitallocate.md" data-raw-source="[&lt;strong&gt;DeviceInitAllocate&lt;/strong&gt;](kmdf-deviceinitallocate.md)"><strong>DeviceInitAllocate</strong></a></p></td>
<td align="left"><p><a href="kmdf-deviceinitallocate.md" data-raw-source="[&lt;strong&gt;DeviceInitAllocate&lt;/strong&gt;](kmdf-deviceinitallocate.md)"> <strong>DeviceInitAllocate</strong> </a>规则指定，对于 PDO 设备或控制设备对象，该框架设备对象初始化方法<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"> <strong>WdfPdoInitAllocate</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"> <strong>WdfControlDeviceInitAllocate</strong> </a>驱动程序调用前，必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-deviceinitapi.md" data-raw-source="[&lt;strong&gt;DeviceInitAPI&lt;/strong&gt;](kmdf-deviceinitapi.md)"><strong>DeviceInitAPI</strong></a></p></td>
<td align="left"><p>对于对 FDO 设备，framework 设备对象初始化方法和 framework FDO 初始化方法必须在调用之前驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong> </a>设备方法对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-doubledeviceinitfree.md" data-raw-source="[&lt;strong&gt;DoubleDeviceInitFree&lt;/strong&gt;](kmdf-doubledeviceinitfree.md)"><strong>DoubleDeviceInitFree</strong></a></p></td>
<td align="left"><p><a href="kmdf-doubledeviceinitfree.md" data-raw-source="[&lt;strong&gt;DoubleDeviceInitFree&lt;/strong&gt;](kmdf-doubledeviceinitfree.md)"> <strong>DoubleDeviceInitFree</strong> </a>规则指定驱动程序应两次释放设备初始化结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-drivercreate.md" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](kmdf-drivercreate.md)"><strong>DriverCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-drivercreate.md" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](kmdf-drivercreate.md)"> <strong>DriverCreate</strong> </a>规则指定使用内核模式驱动程序框架 (KMDF) 的驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate" data-raw-source="[&lt;strong&gt;WdfDriverCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)"> <strong>WdfDriverCreate</strong> </a>方法内创建一个框架驱动程序对象及其<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)"> <strong>DriverEntry</strong> </a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreedevicecallback.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCallback&lt;/strong&gt;](kmdf-initfreedevicecallback.md)"><strong>InitFreeDeviceCallback</strong></a></p></td>
<td align="left"><p>InitFreeDeviceCallback 规则指定一个驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"> <strong>WdfDeviceInitFree</strong> </a>如果驱动程序时遇到错误时它可以初始化新的 framework 设备对象，和驱动程序收到<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"> <strong>WDFDEVICE_INIT</strong> </a>调用结构<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"> <strong>WdfControlDeviceInitAllocate</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-initfreedevicecreate.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreate&lt;/strong&gt;](kmdf-initfreedevicecreate.md)"><strong>InitFreeDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreedevicecreate.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreate&lt;/strong&gt;](kmdf-initfreedevicecreate.md)"> <strong>InitFreeDeviceCreate</strong> </a>规则指定一个驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"> <strong>WdfDeviceInitFree</strong> </a>而不是<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong> </a>如果在一个设备对象初始化方法中发生的错误和驱动程序收到<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"> <strong>WDFDEVICE_INIT</strong> </a>结构通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"> <strong>WdfControlDeviceInitAllocate</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreedevicecreatetype2.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType2&lt;/strong&gt;](kmdf-initfreedevicecreatetype2.md)"><strong>InitFreeDeviceCreateType2</strong></a></p></td>
<td align="left"><p>InitFreeDeviceCreateType2 规则指定一个驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong> </a>它将调用后<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"> <strong>WdfDeviceInitFree</strong> </a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-initfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-initfreedevicecreatetype4.md)"><strong>InitFreeDeviceCreateType4</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-initfreedevicecreatetype4.md)"> <strong>InitFreeDeviceCreateType4</strong> </a>规则指定一个驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"> <strong>WdfDeviceInitFree</strong> </a>如果遇到该驱动程序错误时它将调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong> </a>如果驱动程序收到<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"> <strong>WDFDEVICE_INIT</strong> </a>调用的结构向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"> <strong>WdfControlDeviceInitAllocate</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreenull.md" data-raw-source="[&lt;strong&gt;InitFreeNull&lt;/strong&gt;](kmdf-initfreenull.md)"><strong>InitFreeNull</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreenull.md" data-raw-source="[&lt;strong&gt;InitFreeNull&lt;/strong&gt;](kmdf-initfreenull.md)"> <strong>InitFreeNull</strong> </a>规则指定 DDIs 接收 PWDFDEVICE_INIT 作为参数不能调用使用<strong>NULL</strong>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[WDFDEVICE_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)">WDFDEVICE_INIT</a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctl.md)"><strong>MdlAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p>MdlAfterReqCompletedIntIoctl 规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"> <em>EvtIoInternalDeviceControl</em> </a> I/O 请求之后，无法访问内存描述符列表 (MDL) 的回调函数已完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctla.md)"><strong>MdlAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctla.md)"> <strong>MdlAfterReqCompletedIntIoctlA</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"> <em>EvtIoInternalDeviceControl</em> </a>回调函数I/O 请求完成后，无法访问内存描述符列表 (MDL)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctl.md)"><strong>MdlAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctl.md)"> <strong>MdlAfterReqCompletedIoctl</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"> <em>EvtIoDeviceControl</em> </a>回调函数，内存I/O 请求完成后，不能访问说明符列表 (MDL)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctla.md)"><strong>MdlAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctla.md)"> <strong>MdlAfterReqCompletedIoctlA</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"> <em>EvtIoDeviceControl</em> </a>回调函数，内存I/O 请求完成后，不能访问说明符列表 (MDL)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedRead&lt;/strong&gt;](kmdf-mdlafterreqcompletedread.md)"><strong>MdlAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedRead&lt;/strong&gt;](kmdf-mdlafterreqcompletedread.md)"> <strong>MdlAfterReqCompletedRead</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"> <em>EvtIoRead</em> </a>回调函数，在内存描述符列表 （I/O 请求完成后，不能访问 MDL) 检索到的对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedReadA&lt;/strong&gt;](kmdf-mdlafterreqcompletedreada.md)"><strong>MdlAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedReadA&lt;/strong&gt;](kmdf-mdlafterreqcompletedreada.md)"> <strong>MdlAfterReqCompletedReadA</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"> <em>EvtIoRead</em> </a>回调函数，在内存描述符列表 （I/O 请求完成后，不能访问 MDL) 检索到的对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWrite&lt;/strong&gt;](kmdf-mdlafterreqcompletedwrite.md)"><strong>MdlAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWrite&lt;/strong&gt;](kmdf-mdlafterreqcompletedwrite.md)"> <strong>MdlAfterReqCompletedWrite</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"> <em>EvtIoWrite</em> </a>回调函数、 内存描述符列表I/O 请求完成后，无法访问 (MDL) 检索到的对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-mdlafterreqcompletedwritea.md)"><strong>MdlAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-mdlafterreqcompletedwritea.md)"> <strong>MdlAfterReqCompletedWriteA</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"> <em>EvtIoWrite</em> </a>回调函数、 内存描述符I/O 请求完成后，不能访问列表 (MDL) 检索到的对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedintioctl.md)"><strong>MemAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedintioctl.md)"> <strong>MemAfterReqCompletedIntIoctl</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"> <em>EvtIoInternalDeviceControl</em> </a>回调函数I/O 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedintioctla.md)"><strong>MemAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedintioctla.md)"> <strong>MemAfterReqCompletedIntIoctlA</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"> <em>EvtIoInternalDeviceControl</em> </a>回调函数I/O 请求完成后，不能访问 framework 内存对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedioctl.md)"><strong>MemAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedioctl.md)"> <strong>MemAfterReqCompletedIoctl</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"> <em>EvtIoDeviceControl</em> </a>回调函数，该框架I/O 请求完成后，不能访问内存对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedioctla.md)"><strong>MemAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedioctla.md)"> <strong>MemAfterReqCompletedIoctlA</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"> <em>EvtIoDeviceControl</em> </a>回调函数，该框架I/O 请求完成后，不能访问内存对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedRead&lt;/strong&gt;](kmdf-memafterreqcompletedread.md)"><strong>MemAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedRead&lt;/strong&gt;](kmdf-memafterreqcompletedread.md)"> <strong>MemAfterReqCompletedRead</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"> <em>EvtIoRead</em> </a>回调函数，framework 内存对象I/O 请求完成后，无法访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](kmdf-memafterreqcompletedreada.md)"><strong>MemAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](kmdf-memafterreqcompletedreada.md)"> <strong>MemAfterReqCompletedReadA</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"> <em>EvtIoRead</em> </a>回调函数，framework 内存对象I/O 请求完成后，无法访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWrite&lt;/strong&gt;](kmdf-memafterreqcompletedwrite.md)"><strong>MemAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWrite&lt;/strong&gt;](kmdf-memafterreqcompletedwrite.md)"> <strong>MemAfterReqCompletedWrite</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"> <em>EvtIoWrite</em> </a>回调函数，framework 内存I/O 请求完成后，无法访问对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-memafterreqcompletedwritea.md)"><strong>MemAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-memafterreqcompletedwritea.md)"> <strong>MemAfterReqCompletedWriteA</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"> <em>EvtIoWrite</em> </a>回调函数，framework 内存I/O 请求完成后，无法访问对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullcheck.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheck.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 规则验证驱动程序代码中的 NULL 值不会取消引用驱动程序中更高版本。 如果其中一项条件为 true，此规则将报告缺陷：</p>
<ul>
<li>没有为 NULL，则取消分配更高版本。</li>
<li>一个全局/参数可能为更高版本，取消引用 NULL 的驱动程序中的过程，并且没有显式签入中建议的指针的初始值可能为 NULL 的驱动程序。</li>
</ul>
<p>与 NullCheck 规则冲突，跟踪树窗格中突出显示最相关的代码语句。 有关使用报表输出的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report" data-raw-source="[Static Driver Verifier Report](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report)">静态驱动程序验证工具报告</a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer" data-raw-source="[Understanding the Trace Viewer](https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer)">了解跟踪查看器</a>。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdodeviceinitapi.md" data-raw-source="[&lt;strong&gt;PdoDeviceInitAPI&lt;/strong&gt;](kmdf-pdodeviceinitapi.md)"><strong>PdoDeviceInitAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdodeviceinitapi.md" data-raw-source="[&lt;strong&gt;PdoDeviceInitAPI&lt;/strong&gt;](kmdf-pdodeviceinitapi.md)"> <strong>PdoDeviceInitAPI</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"> <strong>WdfPdoInitAllocate</strong> </a>和所有其他设备对象初始化 DDIs 设置<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"> <strong>WDFDEVICE_INIT</strong> </a>结构为物理设备对象 (PDO) 必须在驱动程序调用之前调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong></a>用于 PDO。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecallback.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCallback&lt;/strong&gt;](kmdf-pdoinitfreedevicecallback.md)"><strong>PdoInitFreeDeviceCallback</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdoinitfreedevicecallback.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCallback&lt;/strong&gt;](kmdf-pdoinitfreedevicecallback.md)"> <strong>PdoInitFreeDeviceCallback</strong> </a>规则指定驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"> <strong>WdfDeviceInitFree</strong> </a>如果发生错误时驱动程序调用任何 framework 设备对象初始化函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreate.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreate&lt;/strong&gt;](kmdf-pdoinitfreedevicecreate.md)"><strong>PdoInitFreeDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreate.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreate&lt;/strong&gt;](kmdf-pdoinitfreedevicecreate.md)"> <strong>PdoInitFreeDeviceCreate</strong> </a>规则指定一个驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"> <strong>WdfDeviceInitFree</strong> </a>而不是<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong> </a>出错时在一个设备对象初始化函数和驱动程序通过调用收到 WDFDEVICE_INIT 结构<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"> <strong>WdfPdoInitAllocate</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreatetype2.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreateType2&lt;/strong&gt;](kmdf-pdoinitfreedevicecreatetype2.md)"><strong>PdoInitFreeDeviceCreateType2</strong></a></p></td>
<td align="left"><p>PdoInitFreeDeviceCreateType2 规则指定一个驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong> </a>它将调用后<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"> <strong>WdfDeviceInitFree</strong> </a>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-pdoinitfreedevicecreatetype4.md)"><strong>PdoInitFreeDeviceCreateType4</strong></a></p></td>
<td align="left"><p>PdoInitFreeDeviceCreateType4 规则指定驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"> <strong>WdfDeviceInitFree</strong> </a>如果驱动程序调用出错<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-controldeviceinitallocate.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAllocate&lt;/strong&gt;](kmdf-controldeviceinitallocate.md)"><strong>ControlDeviceInitAllocate</strong></a></p></td>
<td align="left"><p><a href="kmdf-controldeviceinitallocate.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAllocate&lt;/strong&gt;](kmdf-controldeviceinitallocate.md)"> <strong>ControlDeviceInitAllocate</strong> </a>规则指定对于控制设备对象，该驱动程序都必须调用 framework 设备对象初始化方法<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"> <strong>WdfControlDeviceInitAllocate</strong> </a>驱动程序调用之前<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)"> <strong>WdfDeviceCreate</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-inputbufferapi.md" data-raw-source="[&lt;strong&gt;InputBufferAPI&lt;/strong&gt;](kmdf-inputbufferapi.md)"><strong>InputBufferAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-inputbufferapi.md" data-raw-source="[&lt;strong&gt;InputBufferAPI&lt;/strong&gt;](kmdf-inputbufferapi.md)"> <strong>InputBufferAPI</strong> </a>规则指定中使用的缓冲区检索正确的 DDIs <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"> <em>EvtIoRead</em></a>回调函数。 内<em>EvtIoRead</em>以下 DDIs 不能调用的缓冲区检索回调函数：</p></td>
</tr>
</tbody>
</table>

 

**若要选择 DDI 使用率规则设置**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**DDIUsage**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**DDIUsage.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 






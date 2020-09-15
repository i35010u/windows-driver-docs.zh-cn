---
title: USB 规则集 (KMDF)
description: 使用这些规则验证驱动程序是否正确处理 USB 设备的一些专用 KMDF 方法。
ms.assetid: E07F4E18-CE93-43A8-AAB4-C3CF8CC790CC
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5868ece2ab011b30336256e70d53acb390e3cc89
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103206"
---
# <a name="usb-rule-set-kmdf"></a>USB 规则集 (KMDF)


使用这些规则验证驱动程序是否正确处理 USB 设备的一些专用 KMDF 方法。

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
<td align="left"><p><a href="kmdf-faild0entryiotargetstate.md" data-raw-source="[&lt;strong&gt;FailD0EntryIoTargetState&lt;/strong&gt;](kmdf-faild0entryiotargetstate.md)"><strong>FailD0EntryIoTargetState</strong></a></p></td>
<td align="left"><p><a href="kmdf-faild0entryiotargetstate.md" data-raw-source="[&lt;strong&gt;FailD0EntryIoTargetState&lt;/strong&gt;](kmdf-faild0entryiotargetstate.md)"><strong>FailD0EntryIoTargetState</strong></a>规则指定如果<em>EvtDeviceD0Entry</em>失败，则在<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EvtDeviceD0Entry</em></a>中启动的 USB 连续读取器的 i/o 目标将在同一回调中正确停止。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-usbcontreader.md" data-raw-source="[&lt;strong&gt;UsbContReader&lt;/strong&gt;](kmdf-usbcontreader.md)"><strong>UsbContReader</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbcontreader.md" data-raw-source="[&lt;strong&gt;UsbContReader&lt;/strong&gt;](kmdf-usbcontreader.md)"><strong>UsbContReader</strong></a>规则指定在驱动程序的<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>事件回调函数中正确配置了连续读取器，在该函数中，驱动程序调用<a href="/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeConfigContinuousReader&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)"><strong>WdfUsbTargetPipeConfigContinuousReader</strong></a>方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-usbdevicecreate.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreate&lt;/strong&gt;](kmdf-usbdevicecreate.md)"><strong>UsbDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbdevicecreate.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreate&lt;/strong&gt;](kmdf-usbdevicecreate.md)"><strong>UsbDeviceCreate</strong></a>规则指定不在<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>事件回调函数之外调用<a href="/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate)"><strong>WdfUsbTargetDeviceCreate</strong></a>和<a href="/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a>方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-usbdevicecreatefail.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateFail&lt;/strong&gt;](kmdf-usbdevicecreatefail.md)"><strong>UsbDeviceCreateFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbdevicecreatefail.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateFail&lt;/strong&gt;](kmdf-usbdevicecreatefail.md)"><strong>UsbDeviceCreateFail</strong></a>规则指定如果创建 WDFUSBDEVICE 对象失败，驱动程序从<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>事件回调函数返回并返回错误状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-usbdevicecreatetarget.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateTarget&lt;/strong&gt;](kmdf-usbdevicecreatetarget.md)"><strong>UsbDeviceCreateTarget</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbdevicecreatetarget.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateTarget&lt;/strong&gt;](kmdf-usbdevicecreatetarget.md)"><strong>UsbDeviceCreateTarget</strong></a>规则指定在设备上下文中当前存在的 WDFUSBDEVICE 对象)  (s 时，不会创建多个 WDFUSBDEVICE 对象。</p></td>
</tr>
</tbody>
</table>

 

**选择 Usb 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **Usb**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Usb.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。


---
title: USB 规则集 (KMDF)
description: 使用这些规则验证驱动程序是否正确处理 USB 设备的一些专用 KMDF 方法。
ms.assetid: E07F4E18-CE93-43A8-AAB4-C3CF8CC790CC
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 740118ac0a195fea05b56939c35a17a2c3ce2825
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839996"
---
# <a name="usb-rule-set-kmdf"></a>USB 规则集 (KMDF)


使用这些规则验证驱动程序是否正确处理 USB 设备的一些专用 KMDF 方法。

## <a name="in-this-section"></a>本部分内容


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
<td align="left"><p><a href="kmdf-faild0entryiotargetstate.md" data-raw-source="[&lt;strong&gt;FailD0EntryIoTargetState&lt;/strong&gt;](kmdf-faild0entryiotargetstate.md)"><strong>FailD0EntryIoTargetState</strong></a></p></td>
<td align="left"><p><a href="kmdf-faild0entryiotargetstate.md" data-raw-source="[&lt;strong&gt;FailD0EntryIoTargetState&lt;/strong&gt;](kmdf-faild0entryiotargetstate.md)"><strong>FailD0EntryIoTargetState</strong></a>规则指定如果<em>EvtDeviceD0Entry</em>失败，则在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)"><em>EvtDeviceD0Entry</em></a>中启动的 USB 连续读取器的 i/o 目标将在同一回调中正确停止。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-usbcontreader.md" data-raw-source="[&lt;strong&gt;UsbContReader&lt;/strong&gt;](kmdf-usbcontreader.md)"><strong>UsbContReader</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbcontreader.md" data-raw-source="[&lt;strong&gt;UsbContReader&lt;/strong&gt;](kmdf-usbcontreader.md)"><strong>UsbContReader</strong></a>规则指定在驱动程序的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>事件回调函数中正确配置了连续读取器，在该函数中，驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeConfigContinuousReader&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)"><strong>WdfUsbTargetPipeConfigContinuousReader</strong></a>方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-usbdevicecreate.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreate&lt;/strong&gt;](kmdf-usbdevicecreate.md)"><strong>UsbDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbdevicecreate.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreate&lt;/strong&gt;](kmdf-usbdevicecreate.md)"><strong>UsbDeviceCreate</strong></a>规则指定不在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>事件回调函数之外调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate)"><strong>WdfUsbTargetDeviceCreate</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a>方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-usbdevicecreatefail.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateFail&lt;/strong&gt;](kmdf-usbdevicecreatefail.md)"><strong>UsbDeviceCreateFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbdevicecreatefail.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateFail&lt;/strong&gt;](kmdf-usbdevicecreatefail.md)"><strong>UsbDeviceCreateFail</strong></a>规则指定如果创建 WDFUSBDEVICE 对象失败，驱动程序从<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>EvtDevicePrepareHardware</em></a>事件回调函数返回并返回错误状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-usbdevicecreatetarget.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateTarget&lt;/strong&gt;](kmdf-usbdevicecreatetarget.md)"><strong>UsbDeviceCreateTarget</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbdevicecreatetarget.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateTarget&lt;/strong&gt;](kmdf-usbdevicecreatetarget.md)"><strong>UsbDeviceCreateTarget</strong></a>规则指定在设备上下文中当前存在的 WDFUSBDEVICE 对象泄漏时不会创建多个 WDFUSBDEVICE 对象。</p></td>
</tr>
</tbody>
</table>

 

**选择 Usb 规则集**

1.  在 Microsoft Visual Studio 中选择驱动程序项目（. .Vcxproj）。 在 "**驱动程序**" 菜单中，单击 "**启动静态驱动程序验证程序 ...** "。

2.  单击 "**规则**" 选项卡。在 "**规则集**" 下，选择 " **Usb**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Usb.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[使用静态驱动程序验证器查找驱动程序中的缺陷](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)和[静态驱动程序验证程序命令（MSBuild）](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 






---
title: IrpProcessing 规则集 (KMDF)
description: 使用这些规则验证驱动程序是否正确处理 i/o 请求数据包（IRP）。
ms.assetid: B403F21E-FE35-4A57-92DB-C78FDC1488BD
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3167c18830eaee76975ec5136cfcafd7e42a6731
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839552"
---
# <a name="irpprocessing-rule-set-kmdf"></a>IrpProcessing 规则集 (KMDF)


使用这些规则验证驱动程序是否正确处理 i/o 请求数据包（IRP）。

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
<td align="left"><p><a href="kmdf-fwdirptoioqueuevalid.md" data-raw-source="[&lt;strong&gt;FwdIrpToIoQueueValid&lt;/strong&gt;](kmdf-fwdirptoioqueuevalid.md)"><strong>FwdIrpToIoQueueValid</strong></a></p></td>
<td align="left"><p>规则<a href="kmdf-fwdirptoioqueuevalid.md" data-raw-source="[&lt;strong&gt;FwdIrpToIoQueueValid&lt;/strong&gt;](kmdf-fwdirptoioqueuevalid.md)"><strong>FwdIrpToIoQueueValid</strong></a>指定驱动程序使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpDispatch&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)"><em>EvtDeviceWdmIrpDispatch</em></a>回调或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>EvtDeviceWdmIrpPreprocess</em></a>中的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue" data-raw-source="[&lt;strong&gt;WdfDeviceWdmDispatchIrpToIoQueue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)"><strong>WdfDeviceWdmDispatchIrpToIoQueue</strong></a>方法将 IRP 发送到 i/o 队列。拨.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-setcompletionroutinefromdispatch.md" data-raw-source="[&lt;strong&gt;SetCompletionRoutineFromDispatch&lt;/strong&gt;](kmdf-setcompletionroutinefromdispatch.md)"><strong>SetCompletionRoutineFromDispatch</strong></a></p></td>
<td align="left"><p><a href="kmdf-setcompletionroutinefromdispatch.md" data-raw-source="[&lt;strong&gt;SetCompletionRoutineFromDispatch&lt;/strong&gt;](kmdf-setcompletionroutinefromdispatch.md)"><strong>SetCompletionRoutineFromDispatch</strong></a>规则验证驱动程序是否未从其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpDispatch&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)"><em>EvtDeviceWdmIrpDispatch</em></a>回调函数指定 IRP 上的完成例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-miniportonlywdmdevice.md" data-raw-source="[&lt;strong&gt;MiniportOnlyWdmDevice&lt;/strong&gt;](kmdf-miniportonlywdmdevice.md)"><strong>MiniportOnlyWdmDevice</strong></a></p></td>
<td align="left"><p><a href="kmdf-miniportonlywdmdevice.md" data-raw-source="[&lt;strong&gt;MiniportOnlyWdmDevice&lt;/strong&gt;](kmdf-miniportonlywdmdevice.md)"><strong>MiniportOnlyWdmDevice</strong></a>规则指定 WDF 驱动程序不应使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)"><strong>IoCreateDevice</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure" data-raw-source="[&lt;strong&gt;IoCreateDeviceSecure&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)"><strong>IoCreateDeviceSecure</strong></a>函数创建裸机设备对象。 如果有人尝试将 IRP 发送到 WDM 设备，这将导致计算机崩溃。 这是因为，将设备的 IRP 调度条目设置为特定于 WDF 的条目，但框架尚未创建 WDF 设备。 但微型端口驱动程序可以使用 DDIs，因为没有为其设置驱动程序调度入口点。</p></td>
</tr>
</tbody>
</table>

 

**选择 IrpProcessing 规则集**

1.  在 Microsoft Visual Studio 中选择驱动程序项目（. .Vcxproj）。 在 "**驱动程序**" 菜单中，单击 "**启动静态驱动程序验证程序 ...** "。

2.  单击 "**规则**" 选项卡。在 "**规则集**" 下，选择**IrpProcessing**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**IrpProcessing。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[使用静态驱动程序验证器查找驱动程序中的缺陷](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)和[静态驱动程序验证程序命令（MSBuild）](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 






---
title: USBCAMD2 微型驱动程序操作
description: USBCAMD2 微型驱动程序操作
ms.assetid: 395612cd-3407-4b42-b3a5-0afa838e73d9
keywords:
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- WDK Windows 2000 内核流 USBCAMD2 微型驱动程序操作
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
- Srb WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e363ad5e03a9330bbf6497bb740deb75eeaca2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544623"
---
# <a name="usbcamd2-minidriver-operation"></a>USBCAMD2 微型驱动程序操作

USBCAMD2 照相机微型驱动程序通常运行，如下所示：

- 照相机微型驱动程序调用[ **USBCAMD\_DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff568593)从其[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。 当调用微型驱动程序**USBCAMD\_DriverEntry**，将其传递到 USBCAMD2 微型驱动程序的[ *AdapterReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff554080)回调函数。 USBCAMD2 然后注册使用微型驱动程序*stream.sys*类驱动程序。

- 照相机微型驱动程序可以在接收各种流请求块 (Srb) 及其*AdapterReceivePacket*回调函数来处理，其中包括：
  - [**SRB\_INITIALIZE\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff568185)
  - [**SRB\_初始化\_完成**](https://msdn.microsoft.com/library/windows/hardware/ff568182)
  - [**SRB\_GET\_STREAM\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff568173)
  - [**SRB\_GET\_DEVICE\_PROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff568170)
  - [**SRB\_SET\_DEVICE\_PROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff568204)
  - [**SRB\_GET\_DATA\_INTERSECTION**](https://msdn.microsoft.com/library/windows/hardware/ff568168)
  - [**SRB\_OPEN\_STREAM**](https://msdn.microsoft.com/library/windows/hardware/ff568191)
- 照相机微型驱动程序确定在它必须在如何处理每个 SRB。 微型驱动程序可以调用例程，以帮助处理 Srb USBCAMD2 微型驱动程序库中。 这些例程通常以开头*USBCAMD\_* 前缀。

例如，若要指定照相机微型驱动程序的使用 USBCAMD2 其他回调函数，照相机微型驱动程序指定在其入口点[ **USBCAMD\_设备\_DATA2** ](https://msdn.microsoft.com/library/windows/hardware/ff568590)结构。 然后调用微型驱动程序[ **USBCAMD\_InitializeNewInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff568599)传递初始化的 USBCAMD\_设备\_USBCAMD2 DATA2 结构。 然后，USBCAMD2 调用微型驱动程序的回调函数在必要时。

> [!NOTE]
> [ **USBCAMD\_设备\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568585)仅用于向后兼容性目的在 USBCAMD2 支持结构。

微型驱动程序必须调用[ **USBCAMD\_AdapterReceivePacket** ](https://msdn.microsoft.com/library/windows/hardware/ff568574)将不处理任何 Srb 发送到 USBCAMD2 来处理。

[USBCAMD 库回调函数](https://msdn.microsoft.com/library/windows/hardware/ff568608)描述微型驱动程序实现的回调函数并指明它们是否可选或必需。

以下列表的过程说明了处理 Srb 发送到摄像机微型驱动程序的常规流程：

## <a name="minidrivers-srbinitializedevice-handler"></a>微型驱动程序的 SRB\_初始化\_设备处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>通过调用初始化 USBCAMD2 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568599" data-raw-source="[&lt;strong&gt;USBCAMD_InitializeNewInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568599)"> <strong>USBCAMD_InitializeNewInterface</strong></a>、 指示视频或仍在内核模式下，例如启用设备事件的原始数据处理要求。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>获取 USB 设备和配置描述符。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557605" data-raw-source="[&lt;em&gt;CamConfigureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557605)"> <em>CamConfigureEx</em> </a>回调函数。</p></td>
</tr>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>完成配置。 选择备用设置和最大传输大小。 数组中填充<a href="https://msdn.microsoft.com/library/windows/hardware/ff568623" data-raw-source="[&lt;strong&gt;USBCAMD_Pipe_Config_Descriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568623)"> <strong>USBCAMD_Pipe_Config_Descriptor</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>分析的数组<strong>USBCAMD_Pipe_Config_Descriptor</strong>结构。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557614" data-raw-source="[&lt;em&gt;CamInitialize&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557614)"> <em>CamInitialize</em> </a>回调函数。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>完成初始化。 设置设备电源并激活相机上的默认设置。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>提供的流和流到描述符大小号<em>stream.sys</em>类驱动程序。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbgetstreaminfo-handler"></a>微型驱动程序的 SRB\_获取\_流\_信息处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>提供<a href="https://msdn.microsoft.com/library/windows/hardware/ff559692" data-raw-source="[&lt;strong&gt;HW_STREAM_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559692)"> <strong>HW_STREAM_INFORMATION</strong> </a>流式传输到的信息结构<em>stream.sys</em>类驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>指向设备中的属性集的数组中填写<em>stream.sys</em>类驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff559690" data-raw-source="[&lt;strong&gt;HW_STREAM_HEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559690)"> <strong>HW_STREAM_HEADER</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>填写的流标头中的 pin 的数量。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>如果任何，公开设备事件表。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>修复流信息表中条目的值。 集类别名称 （捕获或仍在）。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>填写到流的属性数组的指针。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbinitializationcomplete-handler"></a>微型驱动程序的 SRB\_初始化\_完成处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>获取有关 USBCAMD2 GUID_USBCAMD_INTERFACE 使用 IRP_MJ_PNP 和 IRP_MN_QUERY_INTERFACE。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbgetdeviceproperty-handler"></a>微型驱动程序的 SRB\_获取\_设备\_属性处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>获取属性的照相机微型驱动程序处理，如<a href="https://msdn.microsoft.com/library/windows/hardware/ff568122" data-raw-source="[PROPSETID_VIDCAP_VIDEOPROCAMP](https://msdn.microsoft.com/library/windows/hardware/ff568122)">PROPSETID_VIDCAP_VIDEOPROCAMP</a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff567802" data-raw-source="[PROPSETID_VIDCAP_CAMERACONTROL](https://msdn.microsoft.com/library/windows/hardware/ff567802)">PROPSETID_VIDCAP_CAMERACONTROL</a>和<a href="https://msdn.microsoft.com/library/windows/hardware/ff568120" data-raw-source="[PROPSETID_VIDCAP_VIDEOCONTROL](https://msdn.microsoft.com/library/windows/hardware/ff568120)">PROPSETID_VIDCAP_VIDEOCONTROL</a>，如以及任何其他自定义属性设置。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbsetdeviceproperty-handler"></a>微型驱动程序的 SRB\_设置\_设备\_属性处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>设置的属性来获取的参数处理相机微型驱动程序<a href="https://msdn.microsoft.com/library/windows/hardware/ff568122" data-raw-source="[PROPSETID_VIDCAP_VIDEOPROCAMP](https://msdn.microsoft.com/library/windows/hardware/ff568122)">PROPSETID_VIDCAP_VIDEOPROCAMP</a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff567802" data-raw-source="[PROPSETID_VIDCAP_CAMERACONTROL](https://msdn.microsoft.com/library/windows/hardware/ff567802)">PROPSETID_VIDCAP_CAMERACONTROL</a>和<a href="https://msdn.microsoft.com/library/windows/hardware/ff568120" data-raw-source="[PROPSETID_VIDCAP_VIDEOCONTROL](https://msdn.microsoft.com/library/windows/hardware/ff568120)">PROPSETID_VIDCAP_VIDEOCONTROL</a>，和任何其他自定义属性集。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbgetdataintersection-handler"></a>微型驱动程序的 SRB\_获取\_数据\_交集处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>返回<a href="https://msdn.microsoft.com/library/windows/hardware/ff561656" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561656)"> <strong>KSDATAFORMAT</strong> </a>结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff561658" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561658)"> <strong>KSDATARANGE</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>检查请求的帧速率 (<strong>VideoInfoHeader.AvgTimePerFrame</strong>) 是所请求的视频格式的上限和下限的限制范围内。 如果超出限制，微型驱动程序应该更正 pSrb-中的以下值&gt;CommandData.IntersectInfo-&gt;Datarange:VideoInfoHeader.AvgTimePerFrame，VideoInfoHeader.dwBitRate。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbopenstream-handler"></a>微型驱动程序的 SRB\_打开\_流处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>验证的视频格式。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>保存照相机微型驱动程序接受的视频格式。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557600" data-raw-source="[&lt;em&gt;CamAllocateBandwidthEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557600)"> <em>CamAllocateBandwidthEx</em> </a>根据视频格式的数据分配带宽和视频格式获取的最大缓冲区大小的回调函数。</p></td>
</tr>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>计算等时通道&#39;s 满足请求的帧速率和输出窗口大小的最大数据包大小。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>选择最接近的替代设置通过调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568625" data-raw-source="[&lt;strong&gt;USBCAMD_SelectAlternateInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568625)"> <strong>USBCAMD_SelectAlternateInterface</strong></a>。 微型驱动程序应为 USBCAMD2 提供可以由照相机的最大可能的帧大小。</p></td>
</tr>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>设置缩放摄像机上的硬件。 将照相机控件设置为在注册表中存储的值或默认设置上，如果第一次。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>确保处于限制范围内的帧速率 (VideoInfoHeader.AvgTimePerFrame) 有关的视频格式，并更正它，如果不是。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557640" data-raw-source="[&lt;em&gt;CamStartCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557640)"> <em>CamStartCaptureEx</em> </a>回调函数。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>设置用于捕获模式下的硬件。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>初始化等时或大容量传输。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbclosestream-handler"></a>微型驱动程序的 SRB\_关闭\_流处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>取消挂起的提交到 USBCAMD2 Irp。 返回所有挂起的到数据 Srb <em>stream.sys</em>类驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>回调函数。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>将停止捕获命令发送到摄像机。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557613" data-raw-source="[&lt;em&gt;CamFreeBandwidthEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557613)"> <em>CamFreeBandwidthEx</em> </a>回调函数来释放同步总线带宽，可能的话。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>选择空闲替代设置。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>释放与 USB 管道相关联的资源。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbuninitializedevice-handler"></a>微型驱动程序的 SRB\_UNINITIALIZE\_设备处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>如果任何流都仍然打开时，关闭它们通过调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff557613" data-raw-source="[&lt;em&gt;CamFreeBandwidthEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557613)"> <em>CamFreeBandwidthEx</em> </a>每个流的回调函数。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557646" data-raw-source="[&lt;em&gt;CamUnInitialize&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557646)"> <em>CamUnInitialize</em> </a>回调函数。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>清除并释放资源。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbsurpriseremoval-handler"></a>微型驱动程序的 SRB\_惊讶\_删除处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>取消挂起的数据 Srb 并返回具有 STATUS_CANCELLED Srb。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff557613" data-raw-source="[&lt;em&gt;CamFreeBandwidthEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557613)"> <em>CamFreeBandwidthEx</em> </a>上所有打开的流的回调函数。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>返回有关任何读/写晚 SRB_SURPRISE_REMOVAL Srb STATUS_CANCELLED。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbsetdataformat-handler"></a>微型驱动程序的 SRB\_设置\_数据\_格式处理程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>验证新的视频格式。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568634" data-raw-source="[&lt;em&gt;USBCAMD_SetVideoFormat&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568634)"> <em>USBCAMD_SetVideoFormat</em></a>。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>关联的流扩展名保存新的格式。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbchangepowerstate-from-power-on-to-power-off-handler"></a>微型驱动程序的 SRB\_更改\_电源\_从启动到关闭电源处理程序状态

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>停止对等时管道如果适用，流式处理或取消仍在进行大容量或中断传输。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>回调函数。</p></td>
</tr>
<tr class="even">
<td><p>照相机微型驱动程序</p></td>
<td><p>将停止捕获命令发送到硬件。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbchangepowerstate-from-power-off-to-power-on-handler"></a>微型驱动程序的 SRB\_更改\_电源\_Power ON 处理程序从关闭电源状态

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Component</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>重新启动同步管道如果适用上, 流式处理或重新提交大容量或中断传输到 USB 类。</p></td>
</tr>
<tr class="odd">
<td><p>照相机微型驱动程序</p></td>
<td><p>还原到正常水平的相机设置和照相机功率消耗。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>回调函数。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>调用微型驱动程序&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff557640" data-raw-source="[&lt;em&gt;CamStartCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557640)"> <em>CamStartCaptureEx</em> </a>回调函数。</p></td>
</tr>
</tbody>
</table>

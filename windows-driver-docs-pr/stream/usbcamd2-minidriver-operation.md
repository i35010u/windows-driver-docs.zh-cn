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
ms.openlocfilehash: 5f94f562f0c91c5d50fe3eb2847fa7a9717637bd
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903731"
---
# <a name="usbcamd2-minidriver-operation"></a>USBCAMD2 微型驱动程序操作

USBCAMD2 照相机微型驱动程序通常运行，如下所示：

- 照相机微型驱动程序调用[ **USBCAMD\_DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_driverentry)从其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。 当调用微型驱动程序**USBCAMD\_DriverEntry**，将其传递到 USBCAMD2 微型驱动程序的[ **AdapterReceivePacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)回调函数。 USBCAMD2 然后注册使用微型驱动程序*stream.sys*类驱动程序。

- 照相机微型驱动程序可以在接收各种流请求块 (Srb) 及其*AdapterReceivePacket*回调函数来处理，其中包括：
  - [**SRB\_INITIALIZE\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialize-device)
  - [**SRB\_初始化\_完成**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialization-complete)
  - [**SRB\_GET\_STREAM\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)
  - [**SRB\_GET\_DEVICE\_PROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-device-property)
  - [**SRB\_SET\_DEVICE\_PROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-device-property)
  - [**SRB\_GET\_DATA\_INTERSECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-data-intersection)
  - [**SRB\_OPEN\_STREAM**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-stream)
- 照相机微型驱动程序确定在它必须在如何处理每个 SRB。 微型驱动程序可以调用例程，以帮助处理 Srb USBCAMD2 微型驱动程序库中。 这些例程通常以开头*USBCAMD\_* 前缀。

例如，若要指定照相机微型驱动程序的使用 USBCAMD2 其他回调函数，照相机微型驱动程序指定在其入口点[ **USBCAMD\_设备\_DATA2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-_usbcamd_device_data2)结构。 然后调用微型驱动程序[ **USBCAMD\_InitializeNewInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)传递初始化的 USBCAMD\_设备\_USBCAMD2 DATA2 结构。 然后，USBCAMD2 调用微型驱动程序的回调函数在必要时。

> [!NOTE]
> [ **USBCAMD\_设备\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-_usbcamd_device_data)仅用于向后兼容性目的在 USBCAMD2 支持结构。

微型驱动程序必须调用[ **USBCAMD\_AdapterReceivePacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)将不处理任何 Srb 发送到 USBCAMD2 来处理。

[**USBCAMD 库回调函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/index#callback-functions)描述微型驱动程序实现的回调函数并指明它们是否可选或必需。

以下列表的过程说明了处理 Srb 发送到摄像机微型驱动程序的常规流程：

## <a name="minidrivers-srbinitializedevice-handler"></a>微型驱动程序的 SRB\_初始化\_设备处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 通过调用初始化 USBCAMD2 [ **USBCAMD_InitializeNewInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)、 指示视频或仍在内核模式下，例如启用设备事件的原始数据处理要求。 |
| 照相机微型驱动程序 | 调用[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 获取 USB 设备和配置描述符。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamConfigureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)回调函数。 |
| 照相机微型驱动程序 | 完成配置。 选择备用设置和最大传输大小。 数组中填充[ **USBCAMD_Pipe_Config_Descriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)结构。 |
| USBCAMD2 | 分析的数组**USBCAMD_Pipe_Config_Descriptor**结构。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_initialize_routine)回调函数。 |
| 照相机微型驱动程序 | 完成初始化。 设置设备电源并激活相机上的默认设置。 |
| USBCAMD2 | 提供的流和流到描述符大小号**stream.sys**类驱动程序。 |

## <a name="minidrivers-srbgetstreaminfo-handler"></a>微型驱动程序的 SRB\_获取\_流\_信息处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 提供[ **HW_STREAM_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_information)流式传输到的信息结构**stream.sys**类驱动程序。 |
| 照相机微型驱动程序 | 指向设备中的属性集的数组中填写**stream.sys**类驱动程序[ **HW_STREAM_HEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_header)结构。 |
| 照相机微型驱动程序 | 调用[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 填写的流标头中的 pin 的数量。 |
| USBCAMD2 | 如果任何，公开设备事件表。 |
| USBCAMD2 | 修复流信息表中条目的值。 集类别名称 （捕获或仍在）。 |
| USBCAMD2 | 填写到流的属性数组的指针。 |

## <a name="minidrivers-srbinitializationcomplete-handler"></a>微型驱动程序的 SRB\_初始化\_完成处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 获取有关 USBCAMD2 GUID_USBCAMD_INTERFACE 使用 IRP_MJ_PNP 和 IRP_MN_QUERY_INTERFACE。 |

## <a name="minidrivers-srbgetdeviceproperty-handler"></a>微型驱动程序的 SRB\_获取\_设备\_属性处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 获取属性的照相机微型驱动程序处理，如[ **PROPSETID_VIDCAP_VIDEOPROCAMP**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)， [ **PROPSETID_VIDCAP_CAMERACONTROL** ](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)，并[ **PROPSETID_VIDCAP_VIDEOCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)，如以及任何其他自定义属性设置。 |

## <a name="minidrivers-srbsetdeviceproperty-handler"></a>微型驱动程序的 SRB\_设置\_设备\_属性处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 设置的属性来获取的参数处理相机微型驱动程序[ **PROPSETID_VIDCAP_VIDEOPROCAMP**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)， [ **PROPSETID_VIDCAP_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)，并[ **PROPSETID_VIDCAP_VIDEOCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)，和任何其他自定义属性集。 |

## <a name="minidrivers-srbgetdataintersection-handler"></a>微型驱动程序的 SRB\_获取\_数据\_交集处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 返回[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)结构[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions//ff561658(v=vs.85))结构。 |
| 照相机微型驱动程序 | 检查请求的帧速率 (**VideoInfoHeader.AvgTimePerFrame**) 是所请求的视频格式的上限和下限的限制范围内。 如果超出限制，微型驱动程序应正确 pSrb 中的以下值-> CommandData.IntersectInfo-> Datarange:VideoInfoHeader.AvgTimePerFrame，VideoInfoHeader.dwBitRate。 |

## <a name="minidrivers-srbopenstream-handler"></a>微型驱动程序的 SRB\_打开\_流处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 验证的视频格式。 |
| 照相机微型驱动程序 | 调用[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 保存照相机微型驱动程序接受的视频格式。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamAllocateBandwidthEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_allocate_bw_routine_ex)根据视频格式的数据分配带宽和视频格式获取的最大缓冲区大小的回调函数。 |
| 照相机微型驱动程序 | 计算满足请求的帧速率和输出窗口大小等时通道的最大数据包大小。 |
| 照相机微型驱动程序 | 选择最接近的替代设置通过调用[ **USBCAMD_SelectAlternateInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_selectalternateinterface)。 微型驱动程序应为 USBCAMD2 提供可以由照相机的最大可能的帧大小。 |
| 照相机微型驱动程序 | 设置缩放摄像机上的硬件。 将照相机控件设置为在注册表中存储的值或默认设置上，如果第一次。 |
| 照相机微型驱动程序 | 确保处于限制范围内的帧速率 (VideoInfoHeader.AvgTimePerFrame) 有关的视频格式，并更正它，如果不是。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamStartCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex)回调函数。 |
| 照相机微型驱动程序 | 设置用于捕获模式下的硬件。 |
| USBCAMD2 | 初始化等时或大容量传输。 |

## <a name="minidrivers-srbclosestream-handler"></a>微型驱动程序的 SRB\_关闭\_流处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 取消挂起的提交到 USBCAMD2 Irp。 返回所有挂起的到数据 Srb **stream.sys**类驱动程序。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)回调函数。 |
| 照相机微型驱动程序 | 将停止捕获命令发送到摄像机。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamFreeBandwidthEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)回调函数来释放同步总线带宽，可能的话。 |
| 照相机微型驱动程序 | 选择空闲替代设置。 |
| USBCAMD2 | 释放与 USB 管道相关联的资源。 |

## <a name="minidrivers-srbuninitializedevice-handler"></a>微型驱动程序的 SRB\_UNINITIALIZE\_设备处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 如果任何流都仍然打开时，关闭它们通过调用微型驱动程序的[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)并[ **CamFreeBandwidthEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)回调对每个流的功能。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamUnInitialize** ](https://docs.microsoft.com/previous-versions//ff557646(v=vs.85))回调函数。 |
| 照相机微型驱动程序 | 清除并释放资源。 |

## <a name="minidrivers-srbsurpriseremoval-handler"></a>微型驱动程序的 SRB\_惊讶\_删除处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 取消挂起的数据 Srb 并返回具有 STATUS_CANCELLED Srb。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)并[ **CamFreeBandwidthEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)上所有打开的流的回调函数。 |
| USBCAMD2 | 返回有关任何读/写晚 SRB_SURPRISE_REMOVAL Srb STATUS_CANCELLED。 |

## <a name="minidrivers-srbsetdataformat-handler"></a>微型驱动程序的 SRB\_设置\_数据\_格式处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 验证新的视频格式。 |
| 照相机微型驱动程序 | 调用[ **USBCAMD_SetVideoFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pfnusbcamd_setvideoformat)。 |
| USBCAMD2 | 关联的流扩展名保存新的格式。 |

## <a name="minidrivers-srbchangepowerstate-from-power-on-to-power-off-handler"></a>微型驱动程序的 SRB\_更改\_电源\_从启动到关闭电源处理程序状态

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 停止对等时管道如果适用，流式处理或取消仍在进行大容量或中断传输。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)回调函数。 |
| 照相机微型驱动程序 | 将停止捕获命令发送到硬件。 |

## <a name="minidrivers-srbchangepowerstate-from-power-off-to-power-on-handler"></a>微型驱动程序的 SRB\_更改\_电源\_Power ON 处理程序从关闭电源状态

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 重新启动同步管道如果适用上, 流式处理或重新提交大容量或中断传输到 USB 类。 |
| 照相机微型驱动程序 | 还原到正常水平的相机设置和照相机功率消耗。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)回调函数。 |
| USBCAMD2 | 调用微型驱动程序的[ **CamStartCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex)回调函数。 |

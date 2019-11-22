---
title: USBCAMD2 微型驱动程序操作
description: USBCAMD2 微型驱动程序操作
ms.assetid: 395612cd-3407-4b42-b3a5-0afa838e73d9
keywords:
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- USBCAMD2 微型驱动程序操作 WDK Windows 2000 内核流式处理
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
- SRBs WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80698d295af72b65c4e948de2d61b0c7180e2ad4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845636"
---
# <a name="usbcamd2-minidriver-operation"></a>USBCAMD2 微型驱动程序操作

USBCAMD2 相机微型驱动程序通常按如下方式操作：

- 照相机微型驱动程序从其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用[**USBCAMD\_DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_driverentry) 。 当微型驱动程序调用**USBCAMD\_DriverEntry**时，它将传递到 USBCAMD2 微型驱动程序的[**AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)回调函数。 然后 *，USBCAMD2 向微型驱动程序类驱动*程序注册该。

- 然后，照相机微型驱动程序可以在其*AdapterReceivePacket*回调函数中接收各种流请求块（SRBs）来处理，其中包括：
  - [**SRB\_初始化\_设备**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialize-device)
  - [**SRB\_初始化\_完成**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialization-complete)
  - [**SRB\_获取\_流\_信息**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)
  - [**SRB\_获取\_设备\_属性**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-device-property)
  - [**SRB\_设置\_设备\_属性**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-device-property)
  - [**SRB\_获取\_交集\_数据**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-data-intersection)
  - [**SRB\_打开\_流**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-stream)
- 相机微型驱动程序确定其必须如何处理每个 SRB。 微型驱动程序可以调用 USBCAMD2 微型驱动程序库中的例程来帮助处理 SRBs。 这些例程通常以*USBCAMD\_* 前缀开头。

例如，若要使用 USBCAMD2 指定相机微型驱动程序的其他回调函数，照相机微型驱动程序将在[**USBCAMD\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_usbcamd_device_data2)中指定其入口点\_DATA2 结构。 然后，微型驱动程序调用[**USBCAMD\_InitializeNewInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)将已初始化的 USBCAMD\_设备\_DATA2 结构传递到 USBCAMD2。 然后，USBCAMD2 会在必要时调用微型驱动程序的回调函数。

> [!NOTE]
> 仅出于向后兼容性的目的，USBCAMD2 支持[**USBCAMD\_设备\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_usbcamd_device_data)结构。

微型驱动程序必须调用[**USBCAMD\_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)将其不处理的任何 SRBs 发送到 USBCAMD2 处理。

[**USBCAMD 库回调函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/index#callback-functions)描述微型驱动程序实现的回调函数，以及它们是可选的还是必需的。

以下过程列表说明了 SRBs 发送到相机微型驱动程序的常规处理流程：

## <a name="minidrivers-srb_initialize_device-handler"></a>微型驱动程序的 SRB\_初始化\_设备处理程序

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 通过调用[**USBCAMD_InitializeNewInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)初始化 USBCAMD2，以指示内核模式下的视频或静止处理要求，例如启用设备事件。 |
| 照相机微型驱动程序 | 调用[**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 获取 USB 设备和配置描述符。 |
| USBCAMD2 | 调用微型驱动程序的[**CamConfigureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)回调函数。 |
| 照相机微型驱动程序 | 完成配置。 选择备用设置和最大传输大小。 填写[**USBCAMD_Pipe_Config_Descriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)结构的数组。 |
| USBCAMD2 | 分析**USBCAMD_Pipe_Config_Descriptor**结构的数组。 |
| USBCAMD2 | 调用微型驱动程序的[**CamInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_initialize_routine)回调函数。 |
| 照相机微型驱动程序 | 完成初始化。 设置设备电源并激活照相机上的默认设置。 |
| USBCAMD2 | 向**stream**类驱动程序提供流和流描述符大小。 |

## <a name="minidrivers-srb_get_stream_info-handler"></a>微型驱动程序的 SRB\_获取\_STREAM\_信息处理程序

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 向**stream**类驱动程序提供[**HW_STREAM_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)流信息结构。 |
| 照相机微型驱动程序 | 在**http.sys**类驱动程序的[**HW_STREAM_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)结构中填写指向设备属性集的数组的指针。 |
| 照相机微型驱动程序 | 调用[**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 填写流标头中的 pin 数目。 |
| USBCAMD2 | 公开设备事件表（如果有）。 |
| USBCAMD2 | 修复流信息表中的条目值。 设置类别名称（捕获或仍为）。 |
| USBCAMD2 | 填写指向流属性数组的指针。 |

## <a name="minidrivers-srb_initialization_complete-handler"></a>微型驱动程序的 SRB\_初始化处理程序\_完成

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 使用 IRP_MJ_PNP 和 IRP_MN_QUERY_INTERFACE 获取 USBCAMD2 GUID_USBCAMD_INTERFACE。 |

## <a name="minidrivers-srb_get_device_property-handler"></a>微型驱动程序的 SRB\_获取\_属性处理程序的\_设备

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 获取照相机微型驱动程序处理的属性，例如[**PROPSETID_VIDCAP_VIDEOPROCAMP**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)、 [**PROPSETID_VIDCAP_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)和[**PROPSETID_VIDCAP_VIDEOCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)，以及任何其他自定义属性集。 |

## <a name="minidrivers-srb_set_device_property-handler"></a>微型驱动程序的 SRB\_\_属性处理程序设置\_设备

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 通过获取[**PROPSETID_VIDCAP_VIDEOPROCAMP**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)、 [**PROPSETID_VIDCAP_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)和[**PROPSETID_VIDCAP_VIDEOCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)的参数以及任何其他自定义属性集来设置相机微型驱动程序处理的属性。 |

## <a name="minidrivers-srb_get_data_intersection-handler"></a>微型驱动程序的 SRB\_获取\_交集处理程序的数据\_

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 返回[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构中的[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构。 |
| 照相机微型驱动程序 | 检查所请求的帧速率（**VideoInfoHeader. AvgTimePerFrame**）是否在请求的视频格式的上限和下限内。 如果超过限制，微型驱动程序应更正 pSrb-> CommandData IntersectInfo-> Datarange： VideoInfoHeader，AvgTimePerFrame 中的以下值。 |

## <a name="minidrivers-srb_open_stream-handler"></a>微型驱动程序的 SRB\_打开\_流处理程序

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 验证视频格式。 |
| 照相机微型驱动程序 | 调用[**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 保存相机微型驱动程序接受的视频格式。 |
| USBCAMD2 | 调用微型驱动程序的[**CamAllocateBandwidthEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_allocate_bw_routine_ex)回调函数以基于视频格式数据分配带宽，并获取视频格式的最大缓冲区大小。 |
| 照相机微型驱动程序 | 计算满足请求的帧速率和输出窗口大小的同步通道的最大数据包大小。 |
| 照相机微型驱动程序 | 通过调用[**USBCAMD_SelectAlternateInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_selectalternateinterface)，选择最近的替代设置。 微型驱动程序应为 USBCAMD2 提供可由相机产生的最大可能帧大小。 |
| 照相机微型驱动程序 | 设置相机上的硬件缩放。 将相机控件设置为注册表中存储的值，或者设置为第一次时的默认设置。 |
| 照相机微型驱动程序 | 确保帧速率（VideoInfoHeader. AvgTimePerFrame）在视频格式限制范围内，如果不是，则更正。 |
| USBCAMD2 | 调用微型驱动程序的[**CamStartCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex)回调函数。 |
| 照相机微型驱动程序 | 将硬件设置为捕获模式。 |
| USBCAMD2 | 初始化同步或大容量传输。 |

## <a name="minidrivers-srb_close_stream-handler"></a>微型驱动程序的 SRB\_关闭\_流处理程序

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 取消挂起的已提交到 USBCAMD2 的 Irp。 将任何挂起的数据 SRBs 返回到**stream**类驱动程序。 |
| USBCAMD2 | 调用微型驱动程序的[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)回调函数。 |
| 照相机微型驱动程序 | 向照相机发送 stop 捕获命令。 |
| USBCAMD2 | 调用微型驱动程序的[**CamFreeBandwidthEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)回调函数以释放同步总线带宽（如果适用）。 |
| 照相机微型驱动程序 | 选择空闲备用设置。 |
| USBCAMD2 | 可用的与 USB 管道关联的资源。 |

## <a name="minidrivers-srb_uninitialize_device-handler"></a>微型驱动程序的 SRB\_取消初始化\_设备处理程序

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 如果任何流仍处于打开状态，请通过对每个流调用微型驱动程序的[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)和[**CamFreeBandwidthEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)回调函数来关闭它们。 |
| USBCAMD2 | 调用微型驱动程序的[**CamUnInitialize**](https://docs.microsoft.com/previous-versions/ff557646(v=vs.85))回调函数。 |
| 照相机微型驱动程序 | 清理和释放资源。 |

## <a name="minidrivers-srb_surprise_removal-handler"></a>微型驱动程序的 SRB\_意外\_删除处理程序

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 取消挂起的数据 SRBs 并返回带有 STATUS_CANCELLED 的 SRBs。 |
| USBCAMD2 | 在所有打开的流上调用微型驱动程序的[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)和[**CamFreeBandwidthEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)回调函数。 |
| USBCAMD2 | 返回 SRB_SURPRISE_REMOVAL 后出现的任何读/写 SRBs 上 STATUS_CANCELLED。 |

## <a name="minidrivers-srb_set_data_format-handler"></a>微型驱动程序的 SRB\_设置\_数据\_格式处理程序

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 验证新的视频格式。 |
| 照相机微型驱动程序 | 调用[**USBCAMD_SetVideoFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pfnusbcamd_setvideoformat)。 |
| USBCAMD2 | 用关联的流扩展保存新格式。 |

## <a name="minidrivers-srb_change_power_state-from-power-on-to-power-off-handler"></a>微型驱动程序的 SRB\_更改电源关闭处理程序\_电源\_状态

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 如果适用，则停止流式传输，或取消挂起的大容量或中断传输。 |
| USBCAMD2 | 调用微型驱动程序的[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)回调函数。 |
| 照相机微型驱动程序 | 向硬件发送停止捕获命令。 |

## <a name="minidrivers-srb_change_power_state-from-power-off-to-power-on-handler"></a>微型驱动程序的 SRB\_从断电到开机处理程序更改\_电源\_状态

| Component | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用[**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 在同步管道上重新启动流式处理（如果适用）或重新提交到 USB 类的批量或中断传输。 |
| 照相机微型驱动程序 | 将相机设置和摄像机功率消耗还原到正常级别。 |
| USBCAMD2 | 调用微型驱动程序的[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)回调函数。 |
| USBCAMD2 | 调用微型驱动程序的[**CamStartCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex)回调函数。 |

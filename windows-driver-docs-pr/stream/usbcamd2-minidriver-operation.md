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
ms.openlocfilehash: 9a5779be49a1bcd47a4e10075e1cea49dd9e9fde
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190139"
---
# <a name="usbcamd2-minidriver-operation"></a>USBCAMD2 微型驱动程序操作

USBCAMD2 相机微型驱动程序通常按如下方式操作：

- 照相机微型驱动程序从其[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用[**USBCAMD \_ DriverEntry**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_driverentry) 。 当微型驱动程序调用 **USBCAMD \_ DriverEntry**时，它将传递到 USBCAMD2 微型驱动程序的 [**AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine) 回调函数。 然后，USBCAMD2 会将微型驱动程序注册到 *stream.sys* 类驱动程序。

- 然后，照相机微型驱动程序可以接收 (SRBs) 在其 *AdapterReceivePacket* 回调函数中处理的各种流请求块，包括：
  - [**SRB \_ 初始化 \_ 设备**](./srb-initialize-device.md)
  - [**SRB \_ 初始化 \_ 完成**](./srb-initialization-complete.md)
  - [**SRB \_ 获取 \_ 流 \_ 信息**](./srb-get-stream-info.md)
  - [**SRB \_ 获取 \_ 设备 \_ 属性**](./srb-get-device-property.md)
  - [**SRB \_ 设置 \_ 设备 \_ 属性**](./srb-set-device-property.md)
  - [**SRB \_ 获取 \_ 数据 \_ 交集**](./srb-get-data-intersection.md)
  - [**SRB \_ 打开 \_ 流**](./srb-open-stream.md)
- 相机微型驱动程序确定其必须如何处理每个 SRB。 微型驱动程序可以调用 USBCAMD2 微型驱动程序库中的例程来帮助处理 SRBs。 这些例程通常以*USBCAMD \_ *前缀开头。

例如，若要使用 USBCAMD2 指定相机微型驱动程序的其他回调函数，照相机微型驱动程序将在 [**USBCAMD \_ 设备 \_ DATA2**](/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_usbcamd_device_data2) 结构中指定其入口点。 然后，微型驱动程序调用 [**USBCAMD \_ InitializeNewInterface**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface) 将已初始化的 USBCAMD \_ 设备 \_ DATA2 结构传递到 USBCAMD2。 然后，USBCAMD2 会在必要时调用微型驱动程序的回调函数。

> [!NOTE]
> [**USBCAMD \_ 设备 \_ 数据**](/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_usbcamd_device_data)结构仅在 USBCAMD2 中受支持，目的是为了向后兼容。

微型驱动程序必须调用 [**USBCAMD \_ AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket) ，以将其未处理的任何 SRBS 发送到 USBCAMD2 处理。

[**USBCAMD 库回调函数**](/windows-hardware/drivers/ddi/usbcamdi/index#callback-functions) 描述微型驱动程序实现的回调函数，以及它们是可选的还是必需的。

以下过程列表说明了 SRBs 发送到相机微型驱动程序的常规处理流程：

## <a name="minidrivers-srb_initialize_device-handler"></a>微型驱动程序的 SRB \_ 初始化 \_ 设备处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 通过调用 [**USBCAMD_InitializeNewInterface**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)初始化 USBCAMD2，以指示内核模式下的视频或静止处理要求，例如启用设备事件。 |
| 照相机微型驱动程序 | 调用 [**USBCAMD_AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 获取 USB 设备和配置描述符。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamConfigureEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex) 回调函数。 |
| 照相机微型驱动程序 | 完成配置。 选择备用设置和最大传输大小。 填写 [**USBCAMD_Pipe_Config_Descriptor**](/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_pipe_config_descriptor) 结构的数组。 |
| USBCAMD2 | 分析 **USBCAMD_Pipe_Config_Descriptor** 结构的数组。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamInitialize**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_initialize_routine) 回调函数。 |
| 照相机微型驱动程序 | 完成初始化。 设置设备电源并激活照相机上的默认设置。 |
| USBCAMD2 | 向 **stream.sys** 类驱动程序提供流和流描述符大小。 |

## <a name="minidrivers-srb_get_stream_info-handler"></a>微型驱动程序的 SRB \_ 获取 \_ 流 \_ 信息处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 向**stream.sys**类驱动程序提供[**HW_STREAM_INFORMATION**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)流信息结构。 |
| 照相机微型驱动程序 | 填写指向 **stream.sys** 类驱动程序 [**HW_STREAM_HEADER**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header) 结构中设备属性集的数组的指针。 |
| 照相机微型驱动程序 | 调用 [**USBCAMD_AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 填写流标头中的 pin 数目。 |
| USBCAMD2 | 公开设备事件表（如果有）。 |
| USBCAMD2 | 修复流信息表中的条目值。 设置类别名称 (捕获或仍) 。 |
| USBCAMD2 | 填写指向流属性数组的指针。 |

## <a name="minidrivers-srb_initialization_complete-handler"></a>微型驱动程序的 SRB \_ 初始化 \_ 完成处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 使用 IRP_MJ_PNP 和 IRP_MN_QUERY_INTERFACE 获取 USBCAMD2 GUID_USBCAMD_INTERFACE。 |

## <a name="minidrivers-srb_get_device_property-handler"></a>微型驱动程序的 SRB \_ 获取 \_ 设备 \_ 属性处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 获取照相机微型驱动程序处理的属性，例如 [**PROPSETID_VIDCAP_VIDEOPROCAMP**](./propsetid-vidcap-videoprocamp.md)、 [**PROPSETID_VIDCAP_CAMERACONTROL**](./propsetid-vidcap-cameracontrol.md)和 [**PROPSETID_VIDCAP_VIDEOCONTROL**](./propsetid-vidcap-videocontrol.md)，以及任何其他自定义属性集。 |

## <a name="minidrivers-srb_set_device_property-handler"></a>微型驱动程序的 SRB \_ 设置 \_ 设备 \_ 属性处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 通过获取 [**PROPSETID_VIDCAP_VIDEOPROCAMP**](./propsetid-vidcap-videoprocamp.md)、 [**PROPSETID_VIDCAP_CAMERACONTROL**](./propsetid-vidcap-cameracontrol.md)和 [**PROPSETID_VIDCAP_VIDEOCONTROL**](./propsetid-vidcap-videocontrol.md)的参数以及任何其他自定义属性集来设置相机微型驱动程序处理的属性。 |

## <a name="minidrivers-srb_get_data_intersection-handler"></a>微型驱动程序的 SRB \_ 获取 \_ 数据 \_ 交集处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 返回[**KSDATARANGE**](/previous-versions/ff561658(v=vs.85))结构中的[**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构。 |
| 照相机微型驱动程序 | 检查所请求的帧速率是否在请求的视频格式的上限和**下限)  (。** 如果超过限制，微型驱动程序应更正 pSrb->CommandData IntersectInfo->Datarange： VideoInfoHeader，AvgTimePerFrame 中的以下值。 |

## <a name="minidrivers-srb_open_stream-handler"></a>微型驱动程序的 SRB \_ 打开 \_ 流处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 验证视频格式。 |
| 照相机微型驱动程序 | 调用 [**USBCAMD_AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 保存相机微型驱动程序接受的视频格式。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamAllocateBandwidthEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_allocate_bw_routine_ex) 回调函数以基于视频格式数据分配带宽，并获取视频格式的最大缓冲区大小。 |
| 照相机微型驱动程序 | 计算满足请求的帧速率和输出窗口大小的同步通道的最大数据包大小。 |
| 照相机微型驱动程序 | 通过调用 [**USBCAMD_SelectAlternateInterface**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_selectalternateinterface)，选择最近的替代设置。 微型驱动程序应为 USBCAMD2 提供可由相机产生的最大可能帧大小。 |
| 照相机微型驱动程序 | 设置相机上的硬件缩放。 将相机控件设置为注册表中存储的值，或者设置为第一次时的默认设置。 |
| 照相机微型驱动程序 | 请确保帧速率 (VideoInfoHeader. AvgTimePerFrame) 在视频格式的限制范围内，如果不是，则更正。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamStartCaptureEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex) 回调函数。 |
| 照相机微型驱动程序 | 将硬件设置为捕获模式。 |
| USBCAMD2 | 初始化同步或大容量传输。 |

## <a name="minidrivers-srb_close_stream-handler"></a>微型驱动程序的 SRB \_ 关闭 \_ 流处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用 [**USBCAMD_AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 取消挂起的已提交到 USBCAMD2 的 Irp。 将任何挂起的数据 SRBs 返回到 **stream.sys** 类驱动程序。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamStopCaptureEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex) 回调函数。 |
| 照相机微型驱动程序 | 向照相机发送 stop 捕获命令。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamFreeBandwidthEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex) 回调函数以释放同步总线带宽（如果适用）。 |
| 照相机微型驱动程序 | 选择空闲备用设置。 |
| USBCAMD2 | 可用的与 USB 管道关联的资源。 |

## <a name="minidrivers-srb_uninitialize_device-handler"></a>微型驱动程序的 SRB \_ 初始化 \_ 设备处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用 [**USBCAMD_AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 如果任何流仍处于打开状态，请通过对每个流调用微型驱动程序的 [**CamStopCaptureEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex) 和 [**CamFreeBandwidthEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex) 回调函数来关闭它们。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamUnInitialize**](/previous-versions/ff557646(v=vs.85)) 回调函数。 |
| 照相机微型驱动程序 | 清理和释放资源。 |

## <a name="minidrivers-srb_surprise_removal-handler"></a>微型驱动程序的 SRB \_ 意外 \_ 删除处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用 [**USBCAMD_AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 取消挂起的数据 SRBs 并返回带有 STATUS_CANCELLED 的 SRBs。 |
| USBCAMD2 | 在所有打开的流上调用微型驱动程序的 [**CamStopCaptureEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex) 和 [**CamFreeBandwidthEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex) 回调函数。 |
| USBCAMD2 | 返回 SRB_SURPRISE_REMOVAL 后出现的任何读/写 SRBs 上 STATUS_CANCELLED。 |

## <a name="minidrivers-srb_set_data_format-handler"></a>微型驱动程序的 SRB \_ 设置 \_ 数据 \_ 格式处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 验证新的视频格式。 |
| 照相机微型驱动程序 | 调用 [**USBCAMD_SetVideoFormat**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pfnusbcamd_setvideoformat)。 |
| USBCAMD2 | 用关联的流扩展保存新格式。 |

## <a name="minidrivers-srb_change_power_state-from-power-on-to-power-off-handler"></a>微型驱动程序的 SRB \_ 更改 \_ 电源 \_ 状态的电源关闭处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用 [**USBCAMD_AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 如果适用，则停止流式传输，或取消挂起的大容量或中断传输。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamStopCaptureEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex) 回调函数。 |
| 照相机微型驱动程序 | 向硬件发送停止捕获命令。 |

## <a name="minidrivers-srb_change_power_state-from-power-off-to-power-on-handler"></a>微型驱动程序的 SRB \_ 将 \_ 电源 \_ 状态从断电更改为开机处理程序

| 组件 | 操作 |
| --- | --- |
| 照相机微型驱动程序 | 调用 [**USBCAMD_AdapterReceivePacket**](/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)。 |
| USBCAMD2 | 在同步管道上重新启动流式处理（如果适用）或重新提交到 USB 类的批量或中断传输。 |
| 照相机微型驱动程序 | 将相机设置和摄像机功率消耗还原到正常级别。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamStopCaptureEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex) 回调函数。 |
| USBCAMD2 | 调用微型驱动程序的 [**CamStartCaptureEx**](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex) 回调函数。 |
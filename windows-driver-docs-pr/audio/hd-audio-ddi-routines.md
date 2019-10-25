---
title: HD 音频 DDI 例程
description: HD 音频 DDI 例程
ms.assetid: 2f360031-39bd-457e-8b64-04b37e21a7fe
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a25edca1c15606c3af3893bcaff5fbc212efd83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831208"
---
# <a name="hd-audio-ddi-routines"></a>HD 音频 DDI 例程


如 HD audio [Ddi 版本之间的差异](https://docs.microsoft.com/windows-hardware/drivers/audio/differences-between-the-hd-audio-ddi-versions)中所述，存在三个版本的 HD audio ddi。 这三个 DDI 版本由[**HDAUDIO\_总线\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)、 [**HDAUDIO\_总线\_接口\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)和[**HDAUDIO\_总线\_接口\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构定义。

这三个 DDI 版本只能在内核模式下进行访问。

每个 DDI 版本都提供对 HD 音频总线控制器管理的硬件资源的访问权限。 这些资源包括编解码器、DMA 引擎、链接带宽、链接位置寄存器和墙壁时钟寄存器。 HD 音频总线驱动程序实现 DDI，并向其子代公开 DDI。 子级是内核模式函数驱动程序的实例，它们使用 DDI 来管理连接到 HD 音频控制器的硬件编解码器。

若要获取对 DDI 版本的访问权限，函数驱动程序必须查询 DDI 上下文对象的 HD 音频总线驱动程序。 有关详细信息，请参阅[获取 HDAUDIO\_总线\_接口 DDI 对象](https://docs.microsoft.com/windows-hardware/drivers/audio/obtaining-an-hdaudio-bus-interface-ddi-object)、[获取 HDAUDIO\_总线\_接口\_V2 DDI 对象](https://docs.microsoft.com/windows-hardware/drivers/audio/obtaining-an-hdaudio-bus-interface-v2-ddi-object)和[获取 HDAUDIO\_总线\_接口\_BDL DDI 对象](https://docs.microsoft.com/windows-hardware/drivers/audio/obtaining-an-hdaudio-bus-interface-bdl-ddi-object)。

三个 DDI 版本中的每个例程均采用指向上下文对象的指针作为第一个调用参数。

HDAUDIO\_总线\_接口结构定义了包含以下例程的 DDI：

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_event_callback)

Windows Vista 和更高版本的 Windows 中提供了 HDAUDIO\_总线\_接口\_V2 结构，它定义了包含以下例程的 DDI：

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateDmaBufferWithNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer_with_notification)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaBufferWithNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer_with_notification)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_event_callback)

[**RegisterNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_notification_event)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_event_callback)

[**UnregisterNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_notification_event)

Windows Vista 和更高版本的 Windows 支持 HD 音频 DDI 的 HDAUDIO\_总线\_接口版本。 此外，还可以在 Windows 2000、Windows XP 和 Windows Server 2003 中安装支持此 DDI 的高清音频总线驱动程序的版本。

HDAUDIO\_总线\_接口\_BDL 结构定义了包含以下例程的 DDI：

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**SetupDmaEngineWithBdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_event_callback)

可在 Windows 2000、Windows XP 和 Windows Server 2003 中安装支持 HDAUDIO\_总线\_接口\_BDL 版本的 HD 音频总线驱动程序的版本。 但是，Windows Vista 不支持此 DDI 版本。

两个 DDIs 中的大部分例程在名称和操作中都相同。 但是，以下两个例程是 DDI 的 HDAUDIO\_总线\_接口版本的一部分，它们不包含在 HDAUDIO\_总线\_接口\_BDL 版本中：

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)

同样，\_HDAUDIO 中的以下三个例程\_接口\_的 BDL 版本不是 HDAUDIO\_总线\_接口版本的一部分：

[**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**SetupDmaEngineWithBdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)

本部分介绍以下 DDI 例程：

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

适用于 PHDAUDIO 的[**SetupDmaEngineWithBdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl) [ **\_BDL\_ISR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-phdaudio_bdl_isr)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_event_callback)

前面的列表包含在其中一个或两个版本中均出现的所有例程。

 

 






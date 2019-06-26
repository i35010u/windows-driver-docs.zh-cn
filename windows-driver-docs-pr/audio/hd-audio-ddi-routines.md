---
title: HD 音频 DDI 例程
description: HD 音频 DDI 例程
ms.assetid: 2f360031-39bd-457e-8b64-04b37e21a7fe
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c81050764092c336862ab4315a7a1fa88c7b93b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359992"
---
# <a name="hd-audio-ddi-routines"></a>HD 音频 DDI 例程


中所述[差异之间 HD 音频 DDI 版本](https://docs.microsoft.com/windows-hardware/drivers/audio/differences-between-the-hd-audio-ddi-versions)，HD 音频 DDI 的三个版本存在。 通过定义以下三个 DDI 版本[ **HDAUDIO\_总线\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)， [ **HDAUDIO\_总线\_接口\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)，和[ **HDAUDIO\_总线\_接口\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构。

三个 DDI 版本都可以访问仅在内核模式下。

每个 DDI 版本提供了对 HD Audio 总线控制器管理的硬件资源的访问。 这些资源包括编解码器、 DMA 引擎、 链路带宽、 链接位置寄存器和墙上时钟注册。 HD Audio 总线驱动程序实现 DDI 并公开与其子 DDI。 子级是使用 DDI 来管理已连接到高清晰度音频控制器的硬件编解码器的内核模式函数驱动程序的实例。

若要获得访问权限 DDI 版本，功能驱动程序必须查询 DDI 上下文对象的 HD Audio 总线驱动程序。 有关详细信息，请参阅[获取 HDAUDIO\_总线\_界面 DDI 对象](https://docs.microsoft.com/windows-hardware/drivers/audio/obtaining-an-hdaudio-bus-interface-ddi-object)，[获取 HDAUDIO\_总线\_接口\_V2 DDI 对象](https://docs.microsoft.com/windows-hardware/drivers/audio/obtaining-an-hdaudio-bus-interface-v2-ddi-object)，并[获取 HDAUDIO\_总线\_接口\_BDL DDI 对象](https://docs.microsoft.com/windows-hardware/drivers/audio/obtaining-an-hdaudio-bus-interface-bdl-ddi-object)。

在三个 DDI 版本中的每个例程将指向上下文对象的指针作为其第一个调用参数。

HDAUDIO\_总线\_接口结构定义包含以下例程 DDI:

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_event_callback)

HDAUDIO\_总线\_接口\_V2 结构也可在 Windows Vista 和更高版本的 Windows，它定义包含以下例程 DDI:

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateDmaBufferWithNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer_with_notification)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaBufferWithNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer_with_notification)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_event_callback)

[**RegisterNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_notification_event)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_event_callback)

[**UnregisterNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_notification_event)

HDAUDIO\_总线\_HD 音频 DDI 界面版本支持 Windows Vista 和更高版本的 Windows 中。 此外，可以在 Windows 2000，Windows XP 和 Windows Server 2003 安装支持此 DDI 的 HD Audio 总线驱动程序的版本。

HDAUDIO\_总线\_接口\_BDL 结构定义包含以下例程 DDI:

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**SetupDmaEngineWithBdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_event_callback)

新版 HD Audio 总线驱动程序支持 HDAUDIO\_总线\_接口\_BDL 版本 HD 音频 DDI 的可以安装在 Windows 2000、 Windows XP 和 Windows Server 2003。 但是，Windows Vista 提供对此 DDI 版本不支持。

在两个 DDIs 例程大部分都是相同的名称和操作。 但是，以下两个例程，属于 HDAUDIO\_总线\_DDI 的界面版本，不包括在 HDAUDIO\_总线\_接口\_BDL 版本：

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer)

同样，下面的三个例程在 HDAUDIO\_总线\_界面\_DDI BDL 版本不属于 HDAUDIO\_总线\_界面版本：

[**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**SetupDmaEngineWithBdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)

本部分介绍以下 DDI 例程：

[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**SetupDmaEngineWithBdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)适用于[ **PHDAUDIO\_BDL\_ISR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-phdaudio_bdl_isr)

[**TransferCodecVerbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-punregister_event_callback)

前面的列表包含在一个或两个版本的 DDI 中出现的所有例程。

 

 






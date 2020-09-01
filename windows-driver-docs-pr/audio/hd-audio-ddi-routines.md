---
title: HD 音频 DDI 例程
description: HD 音频 DDI 例程
ms.assetid: 2f360031-39bd-457e-8b64-04b37e21a7fe
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4102b3f69468e739b2b0fdbcc34265aa3c96b17
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209189"
---
# <a name="hd-audio-ddi-routines"></a>HD 音频 DDI 例程


如 HD audio [Ddi 版本之间的差异](./differences-between-the-hd-audio-ddi-versions.md)中所述，存在三个版本的 HD audio ddi。 这三个 DDI 版本由 [**HDAUDIO \_ 总线 \_ 接口**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)、 [**HDAUDIO \_ 总线 \_ 接口 \_ V2**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)和 [**HDAUDIO \_ 总线 \_ 接口 \_ BDL**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl) 结构定义。

这三个 DDI 版本只能在内核模式下进行访问。

每个 DDI 版本都提供对 HD 音频总线控制器管理的硬件资源的访问权限。 这些资源包括编解码器、DMA 引擎、链接带宽、链接位置寄存器和墙壁时钟寄存器。 HD 音频总线驱动程序实现 DDI，并向其子代公开 DDI。 子级是内核模式函数驱动程序的实例，它们使用 DDI 来管理连接到 HD 音频控制器的硬件编解码器。

若要获取对 DDI 版本的访问权限，函数驱动程序必须查询 DDI 上下文对象的 HD 音频总线驱动程序。 有关详细信息，请参阅 [获取 HDAUDIO \_ BUS \_ 接口 DDI 对象](./obtaining-an-hdaudio-bus-interface-ddi-object.md)、 [获取 HDAUDIO \_ 总线 \_ 接口 \_ V2 DDI](./obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)对象和 [获取 HDAUDIO \_ 总线 \_ 接口 \_ BDL ddi 对象](./obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)。

三个 DDI 版本中的每个例程均采用指向上下文对象的指针作为第一个调用参数。

HDAUDIO \_ 总线 \_ 接口结构定义包含以下例程的 DDI：

[**AllocateCaptureDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateRenderDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**TransferCodecVerbs**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_event_callback)

\_ \_ \_ Windows Vista 和更高版本的 windows 中提供了 HDAUDIO 总线接口 V2 结构，它定义了包含以下例程的 DDI：

[**AllocateCaptureDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateDmaBufferWithNotification**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer_with_notification)

[**AllocateRenderDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaBufferWithNotification**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer_with_notification)

[**FreeDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_event_callback)

[**RegisterNotificationEvent**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_notification_event)

[**SetDmaEngineState**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**TransferCodecVerbs**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_event_callback)

[**UnregisterNotificationEvent**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_notification_event)

\_ \_ Windows Vista 和更高版本的 WINDOWS 支持 HD 音频 DDI 的 HDAUDIO 总线接口版本。 此外，还可以在 Windows 2000、Windows XP 和 Windows Server 2003 中安装支持此 DDI 的高清音频总线驱动程序的版本。

HDAUDIO \_ BUS \_ INTERFACE \_ BDL 结构定义了包含以下例程的 DDI：

[**AllocateCaptureDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateContiguousDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**AllocateRenderDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeContiguousDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**FreeDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**SetupDmaEngineWithBdl**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)

[**TransferCodecVerbs**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_event_callback)

支持 \_ \_ \_ 在 Windows 2000、Windows XP 和 windows Server 2003 中安装 HD 音频的 HDAUDIO 总线接口 BDL 版本的 hd 音频总线驱动程序的版本。 但是，Windows Vista 不支持此 DDI 版本。

两个 DDIs 中的大部分例程在名称和操作中都相同。 但是，以下两个例程是 DDI 的 HDAUDIO \_ 总线 \_ 接口版本的一部分，不包括在 HDAUDIO \_ 总线 \_ 接口 \_ BDL 版本中：

[**AllocateDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**FreeDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)

同样，HDAUDIO 总线接口 BDL 版本中的以下三个例程 \_ \_ \_ 不是 HDAUDIO \_ 总线 \_ 接口版本的一部分：

[**AllocateContiguousDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**FreeContiguousDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**SetupDmaEngineWithBdl**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)

本部分介绍以下 DDI 例程：

[**AllocateCaptureDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)

[**AllocateContiguousDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)

[**AllocateDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer)

[**AllocateRenderDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)

[**ChangeBandwidthAllocation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)

[**FreeContiguousDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)

[**FreeDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)

[**FreeDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_engine)

[**GetDeviceInformation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_device_information)

[**GetLinkPositionRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register)

[**GetResourceInformation**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_resource_information)

[**GetWallClockRegister**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register)

[**RegisterEventCallback**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pregister_event_callback)

[**SetDmaEngineState**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)

[**SetupDmaEngineWithBdl**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)与[ **PHDAUDIO \_ BDL \_ ISR**一起工作的 SetupDmaEngineWithBdl](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-phdaudio_bdl_isr)

[**TransferCodecVerbs**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-ptransfer_codec_verbs)

[**UnregisterEventCallback**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-punregister_event_callback)

前面的列表包含在其中一个或两个版本中均出现的所有例程。

 


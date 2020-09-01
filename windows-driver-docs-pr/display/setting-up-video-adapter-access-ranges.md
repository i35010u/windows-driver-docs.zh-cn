---
title: 设置视频适配器访问范围
description: 设置视频适配器访问范围
ms.assetid: 250c5611-c6f5-49b5-94bc-93a1b43312e6
keywords:
- 视频适配器访问范围 WDK 视频微型端口
- 范围 WDK 视频微型端口
- 逻辑范围用于处理 WDK 视频微型端口
- 适配器访问范围 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a015918d224e2cab82677c06d98ba75f26aa400
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065992"
---
# <a name="setting-up-video-adapter-access-ranges"></a>设置视频适配器访问范围


## <span id="ddk_setting_up_video_adapter_access_ranges_gg"></span><span id="DDK_SETTING_UP_VIDEO_ADAPTER_ACCESS_RANGES_GG"></span>


[**视频 \_ 访问 \_ 范围**](/windows-hardware/drivers/ddi/video/ns-video-_video_access_range)类型元素的数组描述视频适配器对其进行解码的一个或多个内存和/或 i/o 端口的范围。 此数组中的每个访问范围元素都包含与总线相关的物理地址值。

微型端口驱动程序的 [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter) 例程必须声明适配器将响应的所有 PCI 内存和端口或端口范围。 根据[**视频 \_ 端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)中的适配器和**AdapterInterfaceType**值， *HwVidFindAdapter*可以调用以下某些 **VideoPort * * Xxx*函数以获取所需的与总线相关的配置数据：

[**VideoPortGetAccessRanges**](/windows-hardware/drivers/ddi/video/nf-video-videoportgetaccessranges)

[**VideoPortGetBusData**](/windows-hardware/drivers/ddi/video/nf-video-videoportgetbusdata)

[**VideoPortGetDeviceData**](/windows-hardware/drivers/ddi/video/nf-video-videoportgetdevicedata)

[**VideoPortGetRegistryParameters**](/windows-hardware/drivers/ddi/video/nf-video-videoportgetregistryparameters)

[**VideoPortVerifyAccessRanges**](/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges)

如果 *HwVidFindAdapter* 无法通过调用 **VideoPortGetBusData** 或 **VideoPortGetAccessRanges**获取与总线相关的访问范围信息，或从具有 **VideoPortGetDeviceData** 或 **VideoPortGetRegistryParameters**的注册表获取了总线相关的访问范围信息，则微型端口驱动程序应为访问范围提供一组与总线相关的默认值。

每个 *HwVidFindAdapter* 函数都必须将每个已声明的总线相关物理地址范围映射到内核模式地址空间中具有 **VideoPortGetDeviceBase** 逻辑地址范围（特别是在多个总线计算机中）的范围。

使用映射的逻辑范围地址，驱动程序可以调用 **VideoPortRead * * * xxx* 和 **VideoPortWrite * * xxx* 函数来读取或写入适配器。 这些内核模式地址也可以传递到 [**VideoPortCompareMemory**](/windows-hardware/drivers/ddi/video/nf-video-videoportcomparememory)、 [**VideoPortMoveMemory**](/windows-hardware/drivers/ddi/video/nf-video-videoportmovememory)、 [**VideoPortZeroDeviceMemory**](/windows-hardware/drivers/ddi/video/nf-video-videoportzerodevicememory)和/或 [**VideoPortZeroMemory**](/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory)。 对于 i/o 空间中的映射范围，微型端口驱动程序调用 **VideoPortReadPort * * * xxx* 和 **VideoPortWritePort * * xxx* 函数。 对于内存中的映射范围，微型端口驱动程序调用 **VideoPortReadRegister * * * xxx* 和 **VideoPortWriteRegister * * xxx* 函数。

[*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)函数*必须始终*成功调用[**VideoPortVerifyAccessRanges**](/windows-hardware/drivers/ddi/video/nf-video-videoportverifyaccessranges)或[**VideoPortGetAccessRanges**](/windows-hardware/drivers/ddi/video/nf-video-videoportgetaccessranges) ，*才能*调用[**VideoPortGetDeviceBase**](/windows-hardware/drivers/ddi/video/nf-video-videoportgetdevicebase)。

-   对 **VideoPortVerifyAccessRanges** 或 **VideoPortGetAccessRanges** 的任何成功调用都将在特定于总线的视频内存上建立微型端口驱动程序的声明，并在注册表中为其适配器注册地址或 i/o 端口。 但需要注意的是，对 **VideoPortVerifyAccessRanges** 或 **VideoPortGetAccessRanges** 的任何后续调用都将导致该驱动程序以前声明的资源被擦除并替换为传递到最近调用函数的范围。 因此，如果驱动程序声明通过单独调用这些函数来声明范围，则它必须传入所有范围数组，包括已声明的数组。

-   *HwVidFindAdapter* 可以声明适配器的一小部分访问范围，使用此设置来确定该适配器是否为微型端口驱动程序支持的适配器，并为支持的适配器声明一组完整的访问范围，同时调用 **VideoPortGetAccessRanges** 或 **VideoPortVerifyAccessRanges**。 同样，每次成功调用这些 **VideoPort。** 特定适配器的 AccessRanges 例程会在注册表中覆盖调用方的以前的声明。

-   若要声明其他类型的硬件资源（例如中断矢量），微型端口驱动程序应在视频端口配置信息中设置相应的值 \_ \_ \_ 并调用 **VideoPortVerifyAccessRanges**，或者应调用 **VideoPortGetAccessRanges**。

-   若要成功调用 **VideoPortGetAccessRanges** 或 **VideoPortVerifyAccessRanges** ，请确保微型端口驱动程序不会尝试使用已由其他驱动程序使用的寄存器或设备内存地址。

-   在注册表中声明适配器的与总线相关的硬件资源将阻止稍后加载的驱动程序尝试使用相同的访问范围 (和它们的适配器) 的其他硬件资源。 它还会阻止后续加载的驱动程序更改视频适配器的初始化状态。

对旧式资源进行解码的硬件的微型端口驱动程序必须在其 **DriverEntry** 例程中声明这些资源，或者如果已实现，则必须在其 *HwVidLegacyResources* 例程中声明。 旧资源是指未列出在设备 PCI 配置空间中的资源，但被设备解码。 有关详细信息，请参阅 [声明旧资源](claiming-legacy-resources.md) 。

加载微型端口驱动程序并运行其 [*HwVidInitialize*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize) 函数后，将调用微型端口驱动程序的 [*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io) 函数来映射微型端口驱动程序对其相应显示驱动程序可见的视频内存的任何访问范围。

 


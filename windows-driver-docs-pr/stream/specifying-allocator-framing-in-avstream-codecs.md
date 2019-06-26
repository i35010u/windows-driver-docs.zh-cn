---
title: 在 AVStream 编解码器中指定分配器组帧
description: 在 AVStream 编解码器中指定分配器组帧
ms.assetid: e5b042ae-9b9c-48e9-9f0c-449e205316a9
keywords:
- AVStream 硬件编解码器支持 WDK，指定分配器组帧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee5a7aafe9ed991d7b3535ea1b18d0d4ab68d94
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358410"
---
# <a name="specifying-allocator-framing-in-avstream-codecs"></a>在 AVStream 编解码器中指定分配器组帧


通常情况下，KS pin 的分配器要求确定流式处理提供的 AVStream 的缓冲区的物理大小。

但是，因为输入固定只是传递示例下游，输入插针的 KSALLOCATOR 中指定的缓冲区大小要求\_组帧\_EX ([**KS\_组帧\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ks_framing_item).**PhysicalRange**) 未使用。 媒体类型设置并相应地调整其内部结构后，该驱动程序应仍确定输入的帧大小。

尽管驱动程序会在输入的帧大小不能影响固定，最大未完成的帧数 (KS\_组帧\_项。**帧**) 取决插针的分配器要求。 对于平滑流式处理组件和更少的问题在数据流中，我们建议的编码器和解码器的筛选器具有输入和输出固定支持最少三个未完成的框架。

除了提供分配器中的组帧信息之外[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)在设备初始化时，该驱动程序还应更新相关[**KSALLOCATOR\_组帧\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing_ex)结构。 此更新应基于插针的连接中的供应商提供的媒体类型[ *AVStrMiniPinSetDataFormat* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdataformat)回调例程。

 

 





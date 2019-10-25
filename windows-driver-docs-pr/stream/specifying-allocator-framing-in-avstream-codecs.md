---
title: 在 AVStream 编解码器中指定分配器组帧
description: 在 AVStream 编解码器中指定分配器组帧
ms.assetid: e5b042ae-9b9c-48e9-9f0c-449e205316a9
keywords:
- AVStream 硬件编解码器支持 WDK，指定分配器组帧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ccb9b1481fdef6e11bd990047a60a3a434078d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843315"
---
# <a name="specifying-allocator-framing-in-avstream-codecs"></a>在 AVStream 编解码器中指定分配器组帧


通常，KS pin 的分配器要求确定 AVStream 提供的流缓冲区的物理大小。

不过，由于输入插针只传递下游样本，因此在输入插针的 KSALLOCATOR 中指定的缓冲区大小要求\_组帧\_EX （[**KS\_组帧\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ks_framing_item)。**PhysicalRange**）。 设置媒体类型并相应地调整其内部结构后，驱动程序仍应确定输入帧大小。

尽管驱动程序无法影响输入插针上的帧大小，但未完成的帧（KS\_组帧\_项的最大数量。**帧**）取决于 pin 的分配器要求。 对于流式处理组件和更少的故障之间的平滑数据流，建议编码器和解码器筛选器都有输入和输出插针，它们支持至少三个未完成的帧。

除了在[**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)中提供分配器帧信息\_在设备初始化时，驱动程序还应更新相关的[**KSALLOCATOR\_组帧\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)结构。 此更新应基于供应商提供的[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)回调例程中的 pin 连接媒体类型。

 

 





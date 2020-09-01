---
title: 在 AVStream 编解码器中指定分配器组帧
description: 在 AVStream 编解码器中指定分配器组帧
ms.assetid: e5b042ae-9b9c-48e9-9f0c-449e205316a9
keywords:
- AVStream 硬件编解码器支持 WDK，指定分配器组帧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2c2adf3ca3ddeff12ea688bd3b5cd0d44481538
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186303"
---
# <a name="specifying-allocator-framing-in-avstream-codecs"></a>在 AVStream 编解码器中指定分配器组帧


通常，KS pin 的分配器要求确定 AVStream 提供的流缓冲区的物理大小。

但是，因为输入插针只传递下游样本，所以输入插针的 KSALLOCATOR 框架中指定的缓冲区大小要求 \_ \_ ([**KS \_ 组帧 \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ks_framing_item)。**PhysicalRange**不使用 PhysicalRange) 。 设置媒体类型并相应地调整其内部结构后，驱动程序仍应确定输入帧大小。

尽管驱动程序无法影响输入插针上的帧大小，但未完成的帧的最大数目 (KS \_ 组帧 \_ 项。**Frames**) 的帧依赖于 pin 的分配器要求。 对于流式处理组件和更少的故障之间的平滑数据流，建议编码器和解码器筛选器都有输入和输出插针，它们支持至少三个未完成的帧。

除了在 KSPIN 描述符中提供分配器帧信息（ [** \_ \_ 如**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) 设备初始化时间）之外，驱动程序还应更新相关的 [**KSALLOCATOR \_ 组帧 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex) 结构。 此更新应基于供应商提供的 [*AVStrMiniPinSetDataFormat*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat) 回调例程中的 pin 连接媒体类型。

 


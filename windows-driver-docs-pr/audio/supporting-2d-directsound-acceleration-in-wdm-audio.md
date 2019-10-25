---
title: 支持在 WDM 音频中进行 2D DirectSound 加速
description: 支持在 WDM 音频中进行 2D DirectSound 加速
ms.assetid: dbbb2416-8928-41ee-90d5-b3b77d23c251
keywords:
- 硬件加速 WDK DirectSound，二维混合
- 2D 混合 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 489213d8eaec5c02c744bc37cd89f3c917ac6535
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830102"
---
# <a name="supporting-2d-directsound-acceleration-in-wdm-audio"></a>支持在 WDM 音频中进行 2D DirectSound 加速


## <span id="supporting_2d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_2D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound 公开适用于 WDM 音频微型端口驱动程序的硬件加速2D 混合，满足以下要求：

-   小型小型驱动程序包含一个作为 IRP 接收器（KSPIN\_通信\_接收器）的 pin 工厂，在中具有 KSPIN\_数据流的[**KSPIN\_数据流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)方向，并公开数据范围（[**KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)结构），其中说明符（**DataFormat**）。**说明符**成员）设置为 KSDATAFORMAT\_DSOUND\_说明符。

-   Pin 工厂的[**KSPROPERTY\_pin\_CINSTANCES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-cinstances)处理程序将**KSPIN\_CINSTANCES**结构的**PossibleCount**成员设置为大于或等于2的值（对于 KMixer，将始终保留第一个 pin）。 **PossibleCount**值指定当前可从 pin 工厂实例化的 pin 实例数。

-   Pin 工厂必须支持[**KSPROPERTY\_音频\_CPU\_资源**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-cpu-resources)"属性，并且应报告 KSAUDIO\_CPU\_资源\_\_\_主机 cpu，以便为硬件加速。

-   Pin 应满足[DirectSound 节点顺序要求](directsound-node-ordering-requirements.md)。

 

 





---
title: 支持在 WDM 音频中进行 2D DirectSound 加速
description: 支持在 WDM 音频中进行 2D DirectSound 加速
ms.assetid: dbbb2416-8928-41ee-90d5-b3b77d23c251
keywords:
- 硬件加速 WDK DirectSound 2D 混合
- 2D 混合 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a86d410b927d26440d22192694ece5e2642918c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354249"
---
# <a name="supporting-2d-directsound-acceleration-in-wdm-audio"></a>支持在 WDM 音频中进行 2D DirectSound 加速


## <span id="supporting_2d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_2D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound 公开硬件加速 2D 混合的 WDM 音频微型端口驱动程序，满足以下要求：

-   微型端口驱动程序包括一个 pin 工厂，它是 IRP 接收器 (KSPIN\_通信\_接收器)，具有[ **KSPIN\_数据流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-kspin_dataflow) KSPIN方向\_数据流\_中，并公开数据区域 ([**KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)结构) 中的说明符 (**DataFormat**.**说明符**成员) 设置为 KSDATAFORMAT\_说明符\_DSOUND。

-   Pin 工厂[ **KSPROPERTY\_PIN\_CINSTANCES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-cinstances)处理程序集**PossibleCount**隶属**KSPIN\_CINSTANCES**结构为两个或更高版本的值 （始终为 KMixer 保留第一个 pin）。 **PossibleCount**值指定的当前可实例化从 pin 工厂 pin 实例数。

-   Pin 工厂必须支持[ **KSPROPERTY\_音频\_CPU\_资源**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-cpu-resources)属性，并应报告 KSAUDIO\_CPU\_资源\_不\_主机\_CPU 的所有节点的硬件加速。

-   Pin 应满足[DirectSound 节点排序要求](directsound-node-ordering-requirements.md)。

 

 





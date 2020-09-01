---
title: 支持在 WDM 音频中进行 2D DirectSound 加速
description: 支持在 WDM 音频中进行 2D DirectSound 加速
ms.assetid: dbbb2416-8928-41ee-90d5-b3b77d23c251
keywords:
- 硬件加速 WDK DirectSound，二维混合
- 2D 混合 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eac9013b2e8c56017730844c5f1a9f2b9abca2d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210343"
---
# <a name="supporting-2d-directsound-acceleration-in-wdm-audio"></a>支持在 WDM 音频中进行 2D DirectSound 加速


## <span id="supporting_2d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_2D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound 公开适用于 WDM 音频微型端口驱动程序的硬件加速2D 混合，满足以下要求：

-   小型小型驱动程序包含一个 pin 工厂，它是一个 IRP 接收器， (KSPIN \_ 通信 \_ 接收器) ，在中具有 KSPIN 数据流的 [**KSPIN \_ 数据流**](/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow) 方向 \_ \_ ，并公开一个数据范围 ([**KSDATARANGE \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio) 结构) ，其中说明符 (**DataFormat**。**说明符** 成员) 设置为 KSDATAFORMAT \_ 说明符 \_ DSOUND。

-   Pin 工厂的[**KSPROPERTY \_ pin \_ CINSTANCES**](../stream/ksproperty-pin-cinstances.md)处理程序将**KSPIN \_ CINSTANCES**结构的**PossibleCount**成员设置为大于或等于2的值 (第一个 pin 始终保留给 KMixer) 。 **PossibleCount**值指定当前可从 pin 工厂实例化的 pin 实例数。

-   Pin 工厂必须支持 " [**KSPROPERTY \_ 音频 \_ CPU \_ 资源**](./ksproperty-audio-cpu-resources.md) " 属性，并且应 \_ \_ \_ \_ \_ 为硬件加速的所有节点报告 KSAUDIO cpu 资源，而不是 cpu。

-   Pin 应满足 [DirectSound 节点顺序要求](directsound-node-ordering-requirements.md)。

 


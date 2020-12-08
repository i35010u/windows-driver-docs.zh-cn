---
title: WDM 音频驱动程序的基本功能
description: WDM 音频驱动程序的基本功能
keywords:
- WDM 音频驱动程序 WDK，关于 WDM 音频驱动程序
- 音频驱动程序 WDK，关于音频驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9337cc70c865029068a5ff98c22ae2feaf870a4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789367"
---
# <a name="basic-functions-of-a-wdm-audio-driver"></a>WDM 音频驱动程序的基本功能


## <span id="basic_functions_of_a_wdm_audio_driver"></span><span id="BASIC_FUNCTIONS_OF_A_WDM_AUDIO_DRIVER"></span>


Microsoft Windows 驱动模型 (WDM) 音频驱动程序提供以下功能：

-   驱动程序公开所有类型的输入和输出流，以及它可支持的每个流类型的实例数。 驱动程序以一组 pin 工厂和每个工厂可以实例化的 pin 的形式提供此信息。 例如，简单音频设备可能会输入一个 PCM 音频流并输出一个 PCM 音频流。 此设备的筛选器包含两个 pin 工厂：一个用于输入流，一个用于输出流，而每个 pin 工厂仅支持一个 pin 实例。 如果适配器卡只包含其中一个设备，则适配器驱动程序会提供一个筛选器工厂，其中仅包含具有这些功能的筛选器的单个实例。

-   驱动程序支持一个或多个属性集。 例如，所有音频驱动程序都应支持 [KSPROPSETID \_ 音频](./kspropsetid-audio.md)，但某些音频驱动程序也可能支持其他属性集。 驱动程序的客户端使用属性请求来发现筛选器的功能，并更改筛选器的可配置设置。

-   驱动程序可根据需要支持硬件时钟。 此时钟应为可读和可写的，以便流可以与相同或不同硬件上的其他流同步。 有关其他信息，请参阅 [KSPROPSETID \_ 时钟](../stream/kspropsetid-clock.md)。

-   该驱动程序可以选择支持其他媒体接口，如 [**KSINTERFACE \_ standard \_ 流式处理**](../stream/ksinterface-standard-streaming.md)、 [**KSINTERFACE \_ media \_ 波纹 \_ 排队**](../stream/ksinterface-media-wave-queued.md)或 [**KSINTERFACE \_ 标准 \_ 循环 \_ 流式处理**](../stream/ksinterface-standard-looped-streaming.md)。

 


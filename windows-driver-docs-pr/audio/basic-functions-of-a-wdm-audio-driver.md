---
title: WDM 音频驱动程序的基本功能
description: WDM 音频驱动程序的基本功能
ms.assetid: 88013d17-c28c-4c99-9c43-17532f03bfdd
keywords:
- WDM 音频驱动程序 WDK，有关 WDM 音频驱动程序
- 有关音频驱动程序的音频驱动程序 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 729bcad4081e9c24341b7a6511117c1d8a4e15f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568131"
---
# <a name="basic-functions-of-a-wdm-audio-driver"></a>WDM 音频驱动程序的基本功能


## <span id="basic_functions_of_a_wdm_audio_driver"></span><span id="BASIC_FUNCTIONS_OF_A_WDM_AUDIO_DRIVER"></span>


Microsoft Windows 驱动程序模型 (WDM) 的音频驱动程序提供了以下功能：

-   该驱动程序公开的输入和输出流的所有类型和可支持每个流类型的实例数。 该驱动程序中提供这些信息的一组窗体的 pin 工厂和每个工厂可以实例化的 pin 数。 例如，简单的音频设备可能会输入单个 PCM 音频流和输出单个 PCM 音频流。 此设备的筛选器包含两个 pin 工厂-一个用于其中一个输入流的输出流中-和每个 pin 工厂仅支持单个插针实例。 如果适配器卡包含以下设备之一，适配器驱动程序提供了包含单个实例具有这些功能的筛选器的筛选器工厂。

-   该驱动程序支持一个或多个属性集。 例如，支持所有的音频驱动程序应[KSPROPSETID\_音频](https://msdn.microsoft.com/library/windows/hardware/ff537440)，但某些音频驱动程序可能支持以及其他属性集。 该驱动程序的客户端使用属性请求发现筛选器的功能和更改筛选器的可配置设置。

-   该驱动程序可以选择支持硬件时钟。 此时钟应是可读和可写，以便流可以将与相同或不同硬件上其他流同步。 有关其他信息，请参阅[KSPROPSETID\_时钟](https://msdn.microsoft.com/library/windows/hardware/ff566564)。

-   该驱动程序可以选择支持其他媒体接口，如[ **KSINTERFACE\_标准\_流式处理**](https://msdn.microsoft.com/library/windows/hardware/ff563384)， [ **KSINTERFACE\_媒体\_批\_已排队**](https://msdn.microsoft.com/library/windows/hardware/ff563377)，或[ **KSINTERFACE\_标准\_LOOPED\_流式处理**](https://msdn.microsoft.com/library/windows/hardware/ff563381).

 

 





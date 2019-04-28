---
title: 非 PCM 引脚工厂的要求
description: 非 PCM 引脚工厂的要求
ms.assetid: 3ba5da2e-f96f-4645-8a37-dd985287a9f2
keywords:
- 非 PCM 音频格式 WDK，pin 工厂
- pin 工厂 WDK 音频
- 数据交集处理程序 WDK 音频，非 PCM 波形格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9784bf5d3ce72c5cb3811a2c0e82446de748a86a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328687"
---
# <a name="requirements-for-a-non-pcm-pin-factory"></a>非 PCM 引脚工厂的要求


## <span id="requirements_for_a_non_pcm_pin_factory"></span><span id="REQUIREMENTS_FOR_A_NON_PCM_PIN_FACTORY"></span>


在 Windows XP 及更高版本，以及 Microsoft Windows Me，驱动程序播放非 PCM [ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)格式应公开其非 PCM 旋转根据以下指导原则。

首先，定义非 PCM 数据格式，它独立于任何 PCM pin 工厂的 pin 工厂。 因为唯一 pin 实例自动分配给 KMixer PCM 和非 PCM 不能共享相同的单实例 pin 工厂。 如果 pin 工厂支持多个实例，对相同的 pin 工厂可以共存 PCM 和非 PCM。 在这种情况下，但是，您不能保证这些 pin 实例可供非 PCM 客户端在运行时-PCM 客户端可能已具有分配它们。 最安全的选项是为非 PCM 格式提供单独的 pin 工厂。

为了使 pin 来发现并使用 DirectSound 8，已支持 PCM 对筛选器中定义此非 PCM pin 工厂。 否则，DirectSound 将不会检测非 PCM pin。 这也意味着设备不支持 PCM 根本无法支持非 PCM 格式。

其次，实现[交集数据处理程序](proprietary-data-intersection-handlers.md)的非 PCM 插针。 PortCls 提供了内置处理程序，但此默认处理程序始终选择 PCM，因此你应添加自己的非 PCM 格式的处理程序。 不应支持批\_格式\_非 PCM pin 的交集处理程序中的 PCM。 请注意，可以使用调用此处理程序*OutputBufferLength*为 0，在其中用例调用方要求仅对首选的数据范围，不适用于数据本身的大小。 在这种情况下，该处理程序应通过将复制到非 PCM 数据范围的大小进行响应*ResultantFormatLength*参数并返回状态\_缓冲区\_溢出。 Msvad 示例 Windows Driver Kit (WDK) 中包含的代码[ **DataRangeIntersection** ](https://msdn.microsoft.com/library/windows/hardware/ff536764)可用作示例处理程序例程。 若要测试你**DataRangeIntersection**例程，使用[KsStudio 实用工具](ksstudio-utility.md)来实例化您的 pin-它首先调用交集处理程序以确定可接受默认格式。 若要支持非 PCM 格式，您的驱动程序必须正确处理它在以下位置：

-   [**IMiniport::DataRangeIntersection**](https://msdn.microsoft.com/library/windows/hardware/ff536764)

-   微型端口驱动程序的方法**Init**并**NewStream** (有关示例，请参阅[ **IMiniportWavePci::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536734)和[ **IMiniportWavePci::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536735)。)

-   微型端口流方法**SetFormat** (有关示例，请参阅[ **IMiniportWavePciStream::SetFormat**](https://msdn.microsoft.com/library/windows/hardware/ff536732)。)

 

 





---
title: 非 PCM 引脚工厂的要求
description: 非 PCM 引脚工厂的要求
ms.assetid: 3ba5da2e-f96f-4645-8a37-dd985287a9f2
keywords:
- 非 PCM 音频格式 WDK，固定工厂
- 固定工厂的 WDK 音频
- 数据交集处理程序 WDK 音频，非 PCM 波浪格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a7953817a2fe3809abc8fc898bf27a1c95de6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830198"
---
# <a name="requirements-for-a-non-pcm-pin-factory"></a>非 PCM 引脚工厂的要求


## <span id="requirements_for_a_non_pcm_pin_factory"></span><span id="REQUIREMENTS_FOR_A_NON_PCM_PIN_FACTORY"></span>


在 Windows XP 和更高版本以及 Microsoft Windows Me 下，播放非 PCM [**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)格式的驱动程序应按照以下准则公开其非 pcm pin。

首先，为非 PCM 数据格式定义一个独立于任何 PCM 固定工厂的 pin 工厂。 PCM 和非 PCM 不能共享相同的单实例 pin 工厂，因为会自动将唯一的 pin 实例分配给 KMixer。 如果 pin 工厂支持多个实例，则 PCM 和非 PCM 可以共存于同一 pin 工厂。 但是，在这种情况下，不能保证在运行时，在运行时，PCM 客户端可能已分配了这些 pin 实例。 最安全的方法是为非 PCM 格式提供单独的 pin 工厂。

为了 DirectSound 8 发现并使用 pin，请在已支持 PCM 的筛选器上定义此非 PCM 固定工厂。 否则，DirectSound 将无法检测非 PCM pin。 这也意味着，不支持 PCM 的设备不支持非 PCM 格式。

其次，实现非 PCM 插针上的[数据交集处理程序](proprietary-data-intersection-handlers.md)。 PortCls 提供内置处理程序，但此默认处理程序始终选择 PCM，因此，你应该为非 PCM 格式添加自己的处理程序。 不应支持在非 PCM pin 的交集处理程序中\_PCM\_格式。 请注意，可以使用*OutputBufferLength* 0 调用此处理程序，在这种情况下，调用方只请求首选数据范围的大小，而不是数据本身。 在这种情况下，处理程序应通过将非 PCM 数据范围的大小复制到*ResultantFormatLength*参数并返回状态\_缓冲区\_溢出来做出响应。 Windows 驱动程序工具包（WDK）中的 Msvad 示例包含[**DataRangeIntersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)例程的代码，你可以将其用作示例处理程序。 若要测试**DataRangeIntersection**例程，请使用[KsStudio 实用工具](ksstudio-utility.md)来实例化你的 pin--它首先调用交集处理程序，以确定可接受的默认格式。 若要支持非 PCM 格式，你的驱动程序必须在以下位置正确处理它：

-   [**IMiniport：:D ataRangeIntersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)

-   微型端口驱动程序方法**Init**和**newstream.ischecked** （例如，请参阅[**IMiniportWavePci：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)和[**IMiniportWavePci：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)。）

-   微型端口方法**SetFormat** （例如，请参阅[**IMiniportWavePciStream：： SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setformat)。）

 

 





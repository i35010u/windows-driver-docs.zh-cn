---
title: 自定义音频驱动程序类型决策树
description: 自定义音频驱动程序类型决策树
ms.assetid: 7b055baa-1843-4e31-a98e-48b05de94e70
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 979c3247d087ce45384c98a91914595974f82383
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333848"
---
# <a name="custom-audio-driver-type-decision-tree"></a>自定义音频驱动程序类型决策树


步骤 3 中使用此决策树[开发 WDM 音频驱动程序的路线图](roadmap-for-developing-wdm-audio-drivers.md)。 树可帮助您确定的音频驱动程序以了解有关的信息类型。 系统提供的端口类驱动程序 (PortCls) 提供了一组端口驱动程序实现大部分的基本功能。 这些端口驱动程序的驱动程序开发人员简化开发过程。 高清晰度 (HD) 音频和 AC97 驱动程序通常基于 PortCls 类驱动程序，而 USB 和 1394年驱动程序通常基于 AVStream 类。

![用于选择音频驱动程序类型的决策树关系图](images/roadmap-uaacomp.png)

如果您的音频设备基于通用音频体系结构 (UAA) 标准，它与 UAA 兼容。 UAA 兼容音频设备可以使用系统提供 UAA 类驱动程序并不需要自定义驱动程序，但可以提供自己[Windows 音频处理对象](windows-audio-processing-objects.md)。

如果您的音频设备不是 UAA 兼容或它与 UAA 兼容，但你想要实现自定义的功能，您必须决定是否想要开发使用总线 Master DMA 支持驱动程序。 如果你想要提供总线 Master DMA 支持，例如，必须开发基于 PortCls 的音频驱动程序。

有关如何开发自定义音频驱动程序以及如何选择端口驱动程序的信息，请参阅以下主题：

<span id="Custom_Audio_Drivers"></span><span id="custom_audio_drivers"></span><span id="CUSTOM_AUDIO_DRIVERS"></span>[自定义音频驱动程序](custom-audio-drivers.md)  
提供 PortCls 和 AVStream 音频驱动程序的概述，并讨论了每种类型的优缺点。

<span id="AVStream_Overview"></span><span id="avstream_overview"></span><span id="AVSTREAM_OVERVIEW"></span>[AVStream 概述](https://msdn.microsoft.com/library/windows/hardware/ff554240)  
提供了基于 AVStream 驱动程序的体系结构概述，并突出显示的情况下，此类型的驱动程序的最佳选择。

您还必须确定有关音频驱动程序将使用的数据格式和它将支持的格式的范围。 有关数据格式和范围的详细信息，请参阅[音频数据格式和数据区域](audio-data-formats-and-data-ranges.md)。

若要完成的音频驱动程序开发的步骤，请参阅[开发 WDM 音频驱动程序的路线图](roadmap-for-developing-wdm-audio-drivers.md)。

 

 





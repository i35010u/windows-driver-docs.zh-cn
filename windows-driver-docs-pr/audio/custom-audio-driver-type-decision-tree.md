---
title: 自定义音频驱动程序类型决策树
description: 自定义音频驱动程序类型决策树
ms.assetid: 7b055baa-1843-4e31-a98e-48b05de94e70
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64afd65a0d0d6175a09f5bc87cd321b0496fa8cc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208213"
---
# <a name="custom-audio-driver-type-decision-tree"></a>自定义音频驱动程序类型决策树


将此决策树与 [开发 WDM 音频驱动程序的指南](roadmap-for-developing-wdm-audio-drivers.md)的步骤3配合使用。 树可帮助您确定要了解的音频驱动程序的类型。 系统提供的端口类驱动程序 (PortCls) 提供了一组可实现大部分基本功能的端口驱动程序。 这些端口驱动程序简化了驱动程序开发人员的开发过程。 高清晰度 (HD) 音频和 AC97 驱动程序通常基于 PortCls 类驱动程序，而 USB 和1394驱动程序通常基于 AVStream 类。

![选择音频驱动程序类型的决策树关系图](images/roadmap-uaacomp.png)

如果音频设备基于通用音频体系结构 (UAA) standard，则它与 UAA 兼容。 与 UAA 兼容的音频设备可以使用系统提供的 UAA 类驱动程序，不需要自定义驱动程序，但你可以提供自己的 [Windows 音频处理对象](windows-audio-processing-objects.md)。

如果音频设备不 UAA 兼容，或者它是 UAA 兼容的，但你想要实现自定义功能，则必须决定是否要使用总线主机 DMA 支持开发驱动程序。 例如，如果想要提供总线主控 DMA 支持，则必须开发基于 PortCls 的音频驱动程序。

有关如何开发自定义音频驱动程序以及如何选择端口驱动程序的信息，请参阅以下主题：

<span id="Custom_Audio_Drivers"></span><span id="custom_audio_drivers"></span><span id="CUSTOM_AUDIO_DRIVERS"></span>[自定义音频驱动程序](custom-audio-drivers.md)  
概述了 PortCls 和 AVStream 音频驱动程序，并讨论了每种类型的优点和缺点。

<span id="AVStream_Overview"></span><span id="avstream_overview"></span><span id="AVSTREAM_OVERVIEW"></span>[AVStream 概述](../stream/avstream-overview.md)  
提供基于 AVStream 的驱动程序的体系结构概述，并突出显示此类驱动程序是最佳选择的情况。

您还必须确定您的音频驱动程序将使用的数据格式以及它所支持的格式范围。 有关数据格式和范围的详细信息，请参阅 [音频数据格式和数据范围](audio-data-formats-and-data-ranges.md)。

若要完成音频驱动程序开发的步骤，请参阅 [开发 WDM 音频驱动程序的路线图](roadmap-for-developing-wdm-audio-drivers.md)。

 


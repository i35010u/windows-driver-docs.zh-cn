---
title: 硬件卸载的音频的处理
description: 硬件卸载音频处理允许在计算机的主 CPU 之外执行主要音频处理任务。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7d91c09027207d6dc8b4891cc166fa146973b9f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786523"
---
# <a name="span-idaudiohardware-offloaded_audio_processingspanhardware-offloaded-audio-processing"></a><span id="audio.hardware-offloaded_audio_processing"></span>硬件卸载的音频的处理


硬件卸载音频处理允许在计算机的主 CPU 之外执行主要音频处理任务。

音频处理会耗费大量的计算。 在许多情况下，允许专用处理器处理任务（例如混合和应用效果）可能会有好处。 但 Windows 7 和更早版本的 Windows 不支持硬件卸载音频处理。

对于 Windows 8 及更高版本的操作系统，已更新音频驱动程序模型以提供对硬件卸载音频处理的支持，以下部分提供了有关如何开发音频驱动程序的信息，该驱动程序可以公开其处理卸载音频以进行处理的能力。

[体系结构概述](architectural-overview.md)

[已卸载音频的驱动程序实现](driver-implementation-for-offloaded-audio.md)

[针对 SoC 的 PortCls 电源管理更新](portcls-power-management-updates-for-soc.md)

 

 





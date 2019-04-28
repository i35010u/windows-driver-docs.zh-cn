---
title: 硬件卸载的音频的处理
description: 硬件卸载音频处理允许外部计算机的主 CPU 执行主音频处理任务。
ms.assetid: DB20A1D4-F253-4FC0-8445-A92DF5D14605
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c609a573f5149c666023e6b8a50cd66512e7682
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333607"
---
# <a name="span-idaudiohardware-offloadedaudioprocessingspanhardware-offloaded-audio-processing"></a><span id="audio.hardware-offloaded_audio_processing"></span>硬件卸载音频处理


硬件卸载音频处理允许外部计算机的主 CPU 执行主音频处理任务。

音频处理可能是非常需要消耗大量计算密集型操作。 因此在许多情况下，可能有利，可允许的专用的处理器来处理任务，例如，其他处理，例如、 混合，以及应用效果。 但 Windows 7 和 Windows 的早期版本未提供支持的硬件卸载音频处理。

与 Windows 8 和更高版本操作系统中，已更新音频驱动程序模型为硬件卸载音频处理提供支持，以下部分提供有关如何开发可以公开其能够处理的音频驱动程序的信息卸载的音频处理的。

[体系结构概述](architectural-overview.md)

[卸载音频驱动程序实现](driver-implementation-for-offloaded-audio.md)

[SoC PortCls 电源管理更新](portcls-power-management-updates-for-soc.md)

 

 





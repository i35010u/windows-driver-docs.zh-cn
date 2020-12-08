---
title: Windows Vista 对 WDM 音频的支持
description: Windows Vista 对 WDM 音频的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06e6e53f3de5b00e7234f297da39d27110786690
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798713"
---
# <a name="windows-vista-support-for-wdm-audio"></a>Windows Vista 对 WDM 音频的支持


## <span id="windows_xp_support_for_wdm_audio"></span><span id="WINDOWS_XP_SUPPORT_FOR_WDM_AUDIO"></span>


Windows Vista 支持以下 WDM 音频功能：

-   WDM 版本1.40

-   Windows XP 支持的所有功能，但有以下例外。
    -   支持硬件高峰计量，但 Windows Vista 混音器 API 在每个应用程序模式下运行。
    -   Wave 和 MIDI NT4 驱动程序的功能正常，但新的音频用户界面不支持它们。
    -   不支持 AUX 设备，Mmsystem 中的 [**auxGetNumDevs**](/previous-versions/dd756713(v=vs.85)) 函数将始终返回零计数。
    -   不支持 (DRIVERS32) 的 Windows NT4 样式的混音器驱动程序。

 


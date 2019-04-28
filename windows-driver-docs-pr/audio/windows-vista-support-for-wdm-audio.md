---
title: Windows Vista 对 WDM 音频的支持
description: Windows Vista 对 WDM 音频的支持
ms.assetid: a9cf1660-3757-4f8d-82c7-de654bddfb49
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d619ada8fae09ffebf40bc1afcd0220edeb4e8e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335419"
---
# <a name="windows-vista-support-for-wdm-audio"></a>Windows Vista 对 WDM 音频的支持


## <span id="windows_xp_support_for_wdm_audio"></span><span id="WINDOWS_XP_SUPPORT_FOR_WDM_AUDIO"></span>


Windows Vista 支持 WDM 音频功能如下：

-   WDM 版本 1.40

-   Windows XP 支持，但存在以下例外的所有功能。
    -   支持硬件峰值计量，除 Windows Vista 混音器 API 时在每个应用程序模式下运行。
    -   批和 MIDI NT4 驱动程序正常运行，但它们不支持通过新的音频的用户界面。
    -   不支持 AUX 设备，并[ **auxGetNumDevs** ](https://msdn.microsoft.com/library/windows/desktop/dd756713)中 Mmsystem.h 函数将始终返回零计数。
    -   不支持 Windows NT4 样式混音器驱动程序 (DRIVERS32)。

 

 





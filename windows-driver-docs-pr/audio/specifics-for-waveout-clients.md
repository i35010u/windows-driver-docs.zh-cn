---
title: 有关 waveOut 客户端的具体信息
description: 有关 waveOut 客户端的具体信息
ms.assetid: e2cfc59a-0c36-4b57-99e2-b7bed503bc12
keywords:
- waveOut 非 PCM 波形格式 WDK 音频
- 非 PCM 音频格式 WDK，waveOut
- 循环非 PCM 格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4794a7f81cd145a3c3f12af06fe23c545fecbca7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335404"
---
# <a name="specifics-for-waveout-clients"></a>有关 waveOut 客户端的具体信息


## <span id="specifics_for_waveout_clients"></span><span id="SPECIFICS_FOR_WAVEOUT_CLIENTS"></span>


调用[ **waveOutOpen** ](https://msdn.microsoft.com/library/windows/desktop/dd743866)返回 WAVERR\_BADFORMAT 如果驱动程序不支持指定的波形格式。

Microsoft Windows 当前不支持带有非 PCM 格式的批标头的循环。 循环非 PCM 格式的尝试将失败，但系统不会检测失败的标头提交 （不是标头准备） 阶段之前由于体系结构约束。 具体而言，调用[ **waveOutPrepareHeader** ](https://msdn.microsoft.com/library/windows/desktop/dd743868)可能会接受具有 WHDR 的非 PCM 批标头\_BEGINLOOP 和/或 WHDR\_ENDLOOP 中设置**dwFlags**，但随后调用[ **waveOutWrite** ](https://msdn.microsoft.com/library/windows/desktop/dd743876)失败并返回 MMSYSERR\_INVALPARAM。 如果 WHDR\_BEGINLOOP 和 WHDR\_中未设置 ENDLOOP **dwFlags**，但是，指定**dwLoops**&gt;1 不会导致**waveOutWrite**失败。

播放非 PCM 数据时，调用[ **waveOutBreakLoop** ](https://msdn.microsoft.com/library/windows/desktop/dd743854)失败，返回代码 MMSYSERR\_INVALPARAM。

 

 





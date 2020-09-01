---
title: 有关 waveOut 客户端的具体信息
description: 有关 waveOut 客户端的具体信息
ms.assetid: e2cfc59a-0c36-4b57-99e2-b7bed503bc12
keywords:
- waveOut 非 PCM 波纹格式化 WDK 音频
- 非 PCM 音频格式 WDK，waveOut
- 循环非 PCM 格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb531f0af91296687e2e351f5889c078ff92c63d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210399"
---
# <a name="specifics-for-waveout-clients"></a>有关 waveOut 客户端的具体信息


## <span id="specifics_for_waveout_clients"></span><span id="SPECIFICS_FOR_WAVEOUT_CLIENTS"></span>


[**waveOutOpen**](/previous-versions/dd743866(v=vs.85)) \_ 如果驱动程序不支持指定的波形格式，则对 waveOutOpen 的调用将返回 WAVERR BADFORMAT。

Microsoft Windows 当前不支持使用非 PCM 格式的波形标头的循环。 尝试循环的非 PCM 格式将会失败，但系统不会检测到故障，直到标头提交 (不标头准备) 阶段（因为体系结构限制）。 特别是，对[**waveOutPrepareHeader**](/previous-versions/dd743868(v=vs.85))的调用可能会接受 WHDR \_ BEGINLOOP 和/或 WHDR ENDLOOP 设置的非 PCM 波形标头 \_ ，但对[**dwFlags**](/previous-versions/dd743876(v=vs.85))的后续调用会失败，并返回 waveOutWrite **dwFlags** \_ MMSYSERR。 但是，如果 \_ \_ 未在**DWFLAGS**中设置 WHDR BEGINLOOP 和 WHDR ENDLOOP，则指定**DwLoops**1 不会 &gt; 导致**waveOutWrite**失败。

当非 PCM 数据正在播放时，对 [**waveOutBreakLoop**](/previous-versions/dd743854(v=vs.85)) 的调用失败，返回代码为 MMSYSERR \_ INVALPARAM。

 


---
title: 至少有一次音频崩溃的计算机的百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为在 AudioSrv.dll 或 AudioDG.exe 中至少有一次音频崩溃的计算机所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 99e2dcf9c93e10c6aa08b0f565f08e273568346e
ms.sourcegitcommit: 9f6f7d9e327ac3bd34643d8b062e11958a0fe05f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "71195758"
---
# <a name="percent-of-machines-with-at-least-one-audio-crash"></a>至少有一次音频崩溃的计算机的百分比

## <a name="description"></a>描述

请参阅[音频度量](audio-measures.md)中的“音频用户模式可靠性”部分

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |每日，在 7 天内平均|
|度量标准 |计算机百分比|
|最小总体数量 |动态，使用置信区间|
|通过标准 |<= 0.4% 的计算机上的 AudioSrv 至少发生 1 次崩溃<br/><1% 的计算机上的 AudioSrv 或 AudioDG 至少发生 1 次崩溃|
|度量 ID |12518948 - 仅限 AudioSrv<br/>23032999 - AudioSrv 和 AudioDG|

## <a name="calculation"></a>计算

每天：
1. 计算在 AudioSrv 或 AudioDg 中发生崩溃的计算机的数量
1. 计算尝试使用音频的计算机数
1. 发生崩溃的计算机百分比 =（发生崩溃的计算机数）/（尝试使用音频的计算机数）

任何时候该度量的值都是此百分比的七天滚动平均值。
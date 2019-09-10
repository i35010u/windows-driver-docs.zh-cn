---
title: 至少有一次音频崩溃的计算机的百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为在 AudioSrv.dll 或 AudioDG.exe 中至少有一次音频崩溃的计算机所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 28e28f97afcb58fa73eeddd2237e90b20651bb3a
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223919"
---
# <a name="percent-of-machines-with-at-least-one-audio-crash"></a>至少有一次音频崩溃的计算机的百分比

## <a name="description"></a>描述

此度量监视两个服务，即 Windows 音频服务 (AudioSrv.dll) 和音频设备关系图 (AudioDG.exe)，用于检查任一服务是否发生了崩溃   。 如果任一服务发生崩溃，则用户的计算机无法播放任何音频，并且用户必须等待，直到服务恢复才能重新初始化任何音频流。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天|
|度量标准 |计算机百分比|
|最小总体数量 |50 台计算机|
|通过标准 |<= 0.4% 的计算机的任一音频服务至少发生 1 次崩溃|
|度量 ID |12518948|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为在 AudioSrv.dll 或 AudioDG.exe 中至少有一次音频崩溃的计算机所占的百分比 
2. 崩溃的计算机数 = 计数（在 AudioSrv.dll 或 AudioDG.exe 中至少发生一次崩溃的计算机数） 
3. 计算机总数 = 计数（已至少成功初始化 1 个音频流的计算机数） 

### <a name="final-calculation"></a>最终计算

至少有一次音频崩溃的计算机的百分比 = 崩溃的计算机数/计算机总数 
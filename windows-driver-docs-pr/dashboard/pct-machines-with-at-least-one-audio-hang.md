---
title: 至少有一次音频挂起的计算机的百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为在 AudioSrv.dll 或 AudioDG.exe 中至少有一次音频挂起的计算机所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: a9d5f541d94cef56203f0080513258cbe9aba7e0
ms.sourcegitcommit: 9f6f7d9e327ac3bd34643d8b062e11958a0fe05f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "71195756"
---
# <a name="percent-of-machines-with-at-least-one-audio-hang"></a>至少有一次音频挂起的计算机的百分比

## <a name="description"></a>描述

请参阅[音频度量](audio-measures.md)中的“音频用户模式可靠性”

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天|
|度量标准 |计算机的聚合|
|最小总体数量 |50 台计算机|
|通过标准 |<= 1.3 % 的计算机的任一音频服务至少发生 1 次挂起|
|度量 ID |11458540|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为在 AudioSrv.dll 或 AudioDG.exe 中至少有一次音频挂起的计算机所占的百分比  。
2. 挂起的计算机数 = 计数（在 AudioSrv.dll 或 AudioDG.exe 中至少发生 1 次挂起的计算机数） 
3. 计算机总数 = 计数（已至少成功初始化一个音频流的计算机数） 

### <a name="final-calculation"></a>最终计算

至少有一次音频挂起的计算机的百分比 = 挂起的计算机数/计算机总数 
